---
title: "Начало работы с azure WebJobs («задания таймера») для сайтов Office 365 #"
ms.date: 11/03/2017
ms.openlocfilehash: 34adf8616224a7f098f336165f120dcb3cde1a6f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="getting-started-with-azure-webjobs-timer-jobs-for-your-office-365-sites"></a>Начало работы с azure WebJobs («задания таймера») для сайтов Office 365 #

### <a name="summary"></a>Summary ###
В этой записи будет говорить о как можно создавать WebJob Azure в качестве запланированного задания для Office 365 (или на prem должны продолжать) установки SharePoint. В Office 365 при запуске и использовании службы SharePoint Online, вам потребуется повторно думаете способ запуска вещей, которые используются для *задания таймера* в вашей традиционные решения фермы. Понаблюдайте, пока будут рассмотрены основные понятия начало работы по построению настраиваемых заданий для сайтов Office 365.

# <a name="introduction-to-azure-webjob-as-a-timer-job-for-your-office-365-sites"></a>Общие сведения о WebJob Azure как задания таймера для сайтов Office 365 #
В традиционных разработки SharePoint у нас есть [Задания таймера](http://tz.nu/1DNtqH8), который выполняет запланированные в фермы SharePoint. Часто используемый способ — для разработки настраиваемых задания; чтобы постоянно или несколько раз выполнять определенные задачи в вашей среде.

С помощью Office 365 и SharePoint Online у вас нет себе позволить развертывание решений фермы, которой — это обычно проживания задания таймера традиционное письмо. Вместо этого нужно найти другой способ планирования наших задач — это приводит к концепцию [Azure WebJob](http://tz.nu/1ueFvMZ).

## <a name="steps-for-building-the-webjob-using-visual-studio-2015-preview"></a>Шаги по сборке WebJob, с помощью Visual Studio 2015 (Предварительная версия)  ##
Для создания нового WebJob «с нуля», все, что для этого необходимо — создайте новое консольное приложение и убедитесь, что мы добавьте необходимые сборки в проект. В этом примере используется [Visual Studio 2015 (Предварительная версия)](http://tz.nu/1CagngX), как и предполагает его имя в настоящий момент находится в бета-версии.

### <a name="step-1-create-your-console-application"></a>Шаг 1: Создание консольного приложения ###
Сначала необходимо создать новый проект и убедитесь в том, что выбран шаблон «**Консольное приложение**». Кроме того и это важно, убедитесь, что вы выбрали **.NET Framework 4.5**.

![Диалоговое окно Новый проект, задать создание консольного приложения, используя нотацию net Framework 4.5](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/1.Create-Console-Application.png)

### <a name="step-2-add-the-sharepoint-specific-assemblies-from-nuget"></a>Шаг 2: Добавление сборки SharePoint из NuGet ###
Если вы используете Visual Studio 2015 образом, диалоговое окно Диспетчер пакетов NuGet будет выглядеть незначительно отличается от предыдущих версий Visual Studio, но концепцию 's же.

 - Перейдите на «**Сервис**«->»**Диспетчер пакетов NuGet**«->»**Управление пакетами NuGet для решения...**»
 - Поиск для «**приложения для SharePoint**»
 - Установка пакета, называется «**AppForSharePointWebToolkit**» которого будет установить необходимые вспомогательные классы для работы с клиентской объектной модели SharePoint.

![Диспетчер пакетов NuGet диалоговое окно, отображающее условия поиска, приложение для SharePoint. Приложения для SharePoint Web Toolkit выделяется и кнопка установить готова к нажата.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/2.Add-App-For-SharePoint-Web-Toolkit-from-Nuget.png)
Убедитесь, что пакет NuGet работал, проверяя, есть эти два новых классов в проект консольного приложения: ![в обозревателе решений отображается только что добавленный классы контекста точка совместный доступ и вспомогательный.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/3.Project-Overview-With-Added-Files.png)

### <a name="step-3-add-the-required-code-to-execute-the-job-on-your-office-365-site"></a>Шаг 3: Добавление необходимых кода для выполнения задания на сайте Office 365 ###
На этом этапе мы создали наших консольного приложения и мы добавили необходимые сборки, которые легко для нас для взаимодействия с SharePoint. Следующие действия, чтобы использовать эти классы модуля поддержки для выполнения команд в нашей среде SharePoint посредством наших консольное приложение. Установка метки.

***Примечание:*** В образце по завершении работы будет использоваться учетная запись + пароль подход (например, учетная запись службы). Мы обсудим проверки подлинности, параметры, расположенным ниже в статье извлечения и возврата ссылки на другие возможности.

#### <a name="wire-up-the-calls-to-the-sharepoint-online-site-collection"></a>Подключить вызовы семейства сайтов SharePoint Online ####

Следующий код демонстрирует легко подключить звонок на свой сайт, теперь, когда мы добавили вспомогательные классы из пакета наших NuGet.

```C#
 static void Main(string[] args)
  {
      using (ClientContext context = new ClientContext("https://redacted.sharepoint.com"))
      {
          // Use default authentication mode
          context.AuthenticationMode = ClientAuthenticationMode.Default;
          // Specify the credentials for the account that will execute the request
          context.Credentials = new SharePointOnlineCredentials(GetSPOAccountName(), GetSPOSecureStringPassword());

          // TODO: Add your logic here!
      }
  }
 
 
  private static SecureString GetSPOSecureStringPassword()
  {
      try
      {
          Console.WriteLine(" --> Entered GetSPOSecureStringPassword()");
          var secureString = new SecureString();
          foreach (char c in ConfigurationManager.AppSettings["SPOPassword"])
          {
              secureString.AppendChar(c);
          }
          Console.WriteLine(" --> Constructed the secure password");
 
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
          Console.WriteLine(" --> Entered GetSPOAccountName()");
          return ConfigurationManager.AppSettings["SPOAccount"];
      }
      catch
      {
          throw;
      }
   }
``` 

В моем примере приложения видно, что я добавил два вспомогательных метода на извлечение имя учетной записи и пароль для учетной записи в файле app.config. Они рассматриваются в разделе тип проверки подлинности ниже в этой статье.

Для метода главного это все мы потребуется подключить действия до нашей портала. Прежде чем мы узнать подробнее как можно управлять SharePoint из кода, давайте рассмотрим параметры проверки подлинности.

## <a name="authentication-considerations"></a>Сведения о выполнении проверки подлинности ##
Мы будем извлечь два варианта проверки подлинности и посмотрите, их отличий. Могут возникать и другие параметры проверки подлинности в будущем, но ниже приведены два часто используемые подхода.

### <a name="option-1-use-a-service-account-username--password"></a>Вариант 1: Использование учетной записи службы (имя пользователя + пароль) ###
Этот подход довольно прост и позволяет просто введите учетную запись и пароль в клиент Office 365 и затем использовать для примера CSOM для выполнения кода на веб-узлы. Это, отображаемые в примере кода выше также.

#### <a name="create-a-new-service-account-in-office-365"></a>Создание новой учетной записи службы в Office 365 ####
В порядке для работы конкретной учетной записи должен быть создан, который выступает в качестве учетной записи службы — для этого конкретного приложения или универсальные приложения учетную запись, можно использовать все задачи и службы.

Для этой демонстрации я создал новую учетную запись, называется «**SP WebJob**»: ![панель мониторинга показывает только что созданная учетная запись WebJob пакета обновления.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/4.Service-Account-Overview.png)

В зависимости от разрешений задание должно иметь, необходимо изменить разрешения учетной записи при его создании.

#### <a name="store-credentials-in-your-appconfig"></a>Хранение учетных данных в файле app.config ####
В файле app.config проекта можно указать учетные данные, они будут легко fetchable из исполняемый файл программы. Это выглядит как Мои app.config:
```XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
 <startup> 
   <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
 </startup>
 <appSettings>
   <add key="SPOAccount" value="spwebjob@redacted.onmicrosoft.com"/>
   <add key="SPOPassword" value="redacted"/>
 </appSettings>
</configuration>

```
Можно просмотреть два параметра в файле App.config:

 - SPOAccount
 - SPOPassword

При просмотре в первом фрагменте кода я извлечение эти параметры в файле app.config. Имейте в виду, что это означает, что хранения имя учетной записи и пароль в виде простого текста в файле app.config. Необходимо принять решение в проекты как и место для хранения и защиты паролей, следует выбрать этот подход.

#### <a name="the-job-runs-under-the-specified-account"></a>Задание выполняется от имени указанной учетной записи ####
Когда приложение запускается, вы увидите, что он выполняется с помощью учетной записи, указанной в конструкторе SharePointOnlineCredentials():

![В журнале автоматического перевода отображаются четыре атрибутами, WebJob (SP2) для перевода текста.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/5.Running-Job-Overview.png)

В моем примере выше я отображение WebJob, выполняемого действия для настраиваемого списка в одной из личных сайтов, размещенных в SharePoint Online семейство личных сайтов.

Таким образом можно получить хорошее отслеживания изменений в портал, выполняемой наших учетной записи службы. Поэтому важно нужен серьезный подход — имя учетной записи все будут знать, что изменения были автоматически производится наша служба просто, посмотрев метаданных изменены создан.

### <a name="option-2-use-oauth-and-include-authentication-tokens-in-your-requests-to-avoid-specifying-accountpassword"></a>Вариант 2: Использование OAuth и включить маркеры проверки подлинности в запросов не следует использовать учетную запись и пароль ###
Это были подробно описаны в эффективной, мой друг [Кирк Петров](http://blogs.msdn.com/b/kaevans/) в корпорации Майкрософт.

В его учет называемое «[построение надстройки SharePoint как задания таймера](http://tz.nu/1xBA76K)» он объясняется, как можно использовать и проход по access маркеры во избежание настройки имя пользователя и пароль, как я описанного выше, в случае, если вы не хотите хранить пароли и учетные данные в ваше приложение.

## <a name="extending-the-code-with-some-csom-magic"></a>Расширение кода некоторые снег CSOM ##
На этом этапе мы иметь рабочее консольного приложения, который может выполнять проверку подлинности и выполнения запросов к сайтам Office 365. Фигурном ничего не выполнено в коде, поэтому здесь приводится фрагмент для сбора некоторые данные из списка называется «Автоматическое переводы», создавшего я и логики кода будут видеть, есть ли все элементы списка, которые еще не были переведены и затем оно будет выполнения вызова службы перевода и перевода текста для требуемого языка.
```C#
static void Main(string[] args)
{
   try
   {
      Console.WriteLine("Initiating Main()");

      using (ClientContext context = new ClientContext("https://redacted.sharepoint.com"))
      {
         Console.WriteLine("New ClientContext('https://redacted.sharepoint.com') opened. ");

         context.AuthenticationMode = ClientAuthenticationMode.Default;
         context.Credentials = new SharePointOnlineCredentials(GetSPOAccountName(), GetSPOSecureStringPassword());

         Console.WriteLine("Authentication Mode and Credentials configured");

         List translationlist = context.Web.Lists.GetByTitle("Automatic Translations");
         context.Load(translationlist);
         context.ExecuteQuery();

         Console.WriteLine("TranslationList fetched, loaded and ExecuteQuery'ed");

         if (translationlist != null && translationlist.ItemCount > 0)
         {
             Console.WriteLine("The list exist, let's do some magic");

             CamlQuery camlQuery = new CamlQuery();
             camlQuery.ViewXml =
             @"<View>  
             <Query> 
                 <Where><Eq><FieldRef Name='IsTranslated' /><Value Type='Boolean'>0</Value></Eq></Where> 
             </Query> 
         </View>";

             ListItemCollection listItems = translationlist.GetItems(camlQuery);
             context.Load(listItems);
             context.ExecuteQuery();

             Console.WriteLine("Query for listItems executed.");

             foreach (ListItem item in listItems)
             {
                 item["Output"] = TranslatorHelper.GetTranslation(item["Title"], item["Target Language"], item["Original Language"]);
                 item["IsTranslated"] = true;
                 item.Update();
             }


             context.ExecuteQuery();
             Console.WriteLine("Updated all the list items we found. Carry on...");
         }
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

```
Класс **TranslatorHelper** является также вспомогательным классом, который вызывает пользовательский перевода API, но он не обсуждаются подробно в этой записи поскольку это довольно далеко не из области действия.

**Примечание:** Стандарты *, как видно из кода, это демонстрационный ролик и определенно не для рабочей среды, можно изменить его, изменить в соответствии с вашей написания кода и принципов безопасности. Однако все дополнения Console.WriteLine добавляются в порядке для "мне нравится" для просмотра выполнение заданий легко из портала Azure. Подробнее о регистрации и мониторинга ниже в этой статье.*

## <a name="publishing-your-webjob-to-azure"></a>Публикация вашего WebJob в Azure ##
Когда вы разработали вашей WebJob и вы готовы к развертыванию в среде Azure (развертывание на веб-сайт Azure), у вас есть две основные параметры как описано ниже.

### <a name="option-1-upload-a-zip-file-with-the-webjob-binaries-to-your-azure-portal"></a>Вариант 1: Загрузите ZIP-файл с двоичными файлами WebJob в портал Azure ###
Использование портала Azure, где все вашей awesomeness хранить в Azure, можно будет загрузить zip файл, содержащий выходные данные построения Visual Studio. Это удобный способ компиляции и доставки кода другому человеку пользователей, которые будут выполнять развертывание для вас.

#### <a name="create-the-zip-file"></a>Создание ZIP-файла ####
Просто скопировать все, что построение выходные файлы из Visual Studio (обычно в папке bin/Debug или bin/Release):

![Откроется представление проводника Windows из папки bin/Debug.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/6.Zip-File-Overview.png)
Сжать их, поэтому вы получите замечательно ZIP-файл для задания web:

![Откроется представление проводника Windows из завершенных ZIP-файл.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/7.Zip-File-Created.png)

#### <a name="find-a-web-site-where-the-job-should-be-deployed"></a>Найдите веб-сайт, где должны развертываться задания ####

Итак, теперь у вас есть пакет. Это довольно легко. Следующим шагом является заголовок вход в систему https://portal.azure.com и входа в систему на портале Windows Azure. Отсюда вам потребуется создать новый веб-сайт или использовать существующее — этот веб-сайт будет узла для нашего web задания.

В моем случае у меня уже есть веб-сайта Azure для некоторых демонстрационных Мой Office 365 так просто используете его.

Прокрутите вниз в области Параметры для веб-сайта можно найти так называемых «**WebJobs**» в разделе «**операции**» заголовок:

![Портал Azure автора отображается со стрелкой WebJobs. ](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/8.Find-WebJobs-in-Azure-Portal.png)
 **Click, где стрелка!**

#### <a name="upload-your-webjob"></a>Отправка ваше WebJob ####

Загрузите свою работу в web, нажав кнопку входа **[+ Добавить]** :

![Портал WebJobs Azure отображается со стрелкой добавить.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/9.Upload-Azure-WebJob-from-Azure-Portal.png)

Выберите имя, как выполняется задание и фактических ZIP-файла:

![Откроется диалоговое окно Добавление WebJob. В поле имя содержит текст Zimmergren-O365-WebJobSample и способ выполнения поле содержит текст по запросу.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/10.Configure-Name-of-Uploaded-WebJob.png)

***Важные:*** На этом этапе альтернатива «Для выполнения» только обеспечивает «По требованию» или «Продолжить», но скоро будет поддержка «Расписание» также – которого — это действительно необходимо.

*(Подсказка: В следующем разделе для публикации на самом Azure, можно запланировать его из внутри VS).*

Да выполнить – теперь можно запустить вашей webjob через портал Azure:

![Портал WebJobs Azure отображается со списком новых заданий. Контекстное меню появляется над задания с параметрами выполнения и удалить.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/11.Run-WebJob-from-Azure-Portal.png)

Хотя это все нормально и замечательно, поскольку портала отсутствуют диалоговые окна для поддержки планирования пока — я бы настоятельно рекомендуется извлечь как опубликовать из внутри Visual Studio 2015 вместо (или 2013, если это ваш выбор).

### <a name="option-2-publish-directly-to-azure-from-visual-studio"></a>Вариант 2: Публикация непосредственно в Azure из Visual Studio ###
Это Мои избранные один на этом этапе так, как я могу использовать инструментарий в Visual Studio для быстро публиковать все изменения непосредственно в моей размещенной службы. Другие преимущество станет снимите флажок ближайшее время, как можно планировать задания точно способ для выполнения непосредственно из диалоговых окон в Visual Studio.

#### <a name="choose-to-publish-the-webjob-from-visual-studio-2015"></a>Выберите публикация WebJob из Visual Studio 2015 ####

***Примечание:*** *Этих диалоговых окон может немного отличаться при запуске более ранней версии Visual Studio. Кроме того я уже вошел, если вы выполняете это в первый раз появляется диалоговое окно входа для входа в учетную запись Azure. Который является подготовкой.*

Просто щелкните правой кнопкой мыши проект и выберите пункт «**Публикация Azure WebJob...**»:

![В контекстном меню в окне Обозреватель решений будет отображаться с публикация Azure WebJob выделенным параметром.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/12.Publish-WebJob-from-Visual-Studio-2015.png)

#### <a name="add-azure-webjob"></a>Добавление Azure WebJob ####
Откроется в диалоговом окне нового там, где можно настроить задания, а так как мы хотели повторяющегося задания, которое должно выполняться по расписанию (в моем случае один раз каждую ночь) можно настроить расписание непосредственно из диалоговых окон: ![displ — это диалоговое окно Добавление WebJob Azure ayed. В поле имя WebJob содержит текст Zimmergren O365 WebJobSample, в поле режим запуска WebJob содержит параметр выполнения по расписанию, повторяющееся поле содержит задания типовой параметр и установлен флажок Нет даты окончания, повторять каждое поле установлено значение 1 дня , а начальную дату — 9 Januari 2015.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/13.Add-Azure-WebJob-Dialog.png)

 - Убедитесь, что имя является понятное веб-сайт
 - Режим выполнения, я на «Запуск расписание», так как требуется, чтобы оно только на определенное время каждый день
 - Задание должно быть повторяющееся задание или разовое задание? Поскольку необходимо моделирования задания таймера, он должен быть повторяющаяся, и в моем случае без любая Дата завершения, так как она будет запущена каждую ночь
 - Вы хотите, можно планировать повторения вниз до каждую минуту.
 - Когда нужно начинать? :-)

Счетчик **ОК** и вы увидите, что Visual Studio уменьшится сообщение «**Установка WebJobs публикации NuGet пакет**».

#### <a name="visual-studio-added-webjobs-publishing-nuget-package"></a>Visual Studio добавлены WebJobs публикации NuGet-пакет ####
![Отображается диалоговое окно WebJobs NuGet пакет установки, которое отображает счетчик и текст, установка WebJobs публикации NuGet пакета.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/14.WebJobs-NuGet-Package-Install.png)

Это фактически добавляет новый файл с именем «**Публикация settings.json webjob**» для проектов, содержащий конфигурации для задания.

Файл выглядит следующим образом:
```json
{
  "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
  "webJobName": "Zimmergren-O365-WebJobSample",
  "startTime": "2015-01-09T01:00:00+01:00",
  "endTime": null,
  "jobRecurrenceFrequency": "Day",
  "interval": 1,
  "runMode": "Scheduled"
}
```
Права не требуется беспокоить с помощью данного файла в данный момент, поскольку уже предназначена планирования с помощью диалоговых окон.

#### <a name="select-publishingdeployment-target"></a>Выбор целевого публикации и развертывание ####
Следующим шагом в диалоговом окне будет места публикации/развертывания вашей WebJob. Можно импортировать профиль публикации или выберите веб-узлов Microsoft Azure для проверки подлинности и выберите один из существующих сайтов.

Поскольку у меня правило всегда загрузка Мои публикации профили из портала личных Azure я будет пойти дальше и выберите «**Импорт**» и просто указать публикации файла профиля, который я загружен из личных веб-сайта Azure:

![На вкладке подключения к видимым отображается диалоговое окно Публикация веб-сайта.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/15.Publish-Web-Dialog.png)

После этого все, что для этого необходимо — нажмите кнопку «Опубликовать». Не следует бояться, оно не байтового. Я думаю.

#### <a name="publish"></a>Публикация ####
После нажатия кнопки Опубликовать диалоговое окно Публикация веб-трафик будет отображать ход выполнения задания Web развертывания: ![диалоговое окно, отображается действие опубликовать Web.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/16.Publish-Progress-Visual-Studio-2015.png)

После завершения, вы должны увидеть WebJob в портал Azure: ![портала Azure отображается Zimmergren O365 WebJobSample в списке WebJobs в состоянии, завершения 2 минут назад.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/17.Web-Job-Published-as-seen-in-Azure-Portal.png)

Состояние WebJob теперь отображается как завершено. Он будет сказать сбоев и сообщений об ошибках, если он будет любой необработанное исключение или для предоставления неработоспособные поведение.

По-прежнему написано «По запросу», но это задание выполняется один раз каждый час теперь.

## <a name="monitoring-the-job-and-reviewing-logs"></a>Мониторинг задания и просмотра журналов ##
Если вы сделали все предыдущие действия, у вас работают как запланированная задача в облаке, задание для выполнения действий к вашей сайтов Office 365.

### <a name="view-all-job-executions-and-status"></a>Просмотр всех заданий выполнений и состояния ###
Если вы хотите просмотреть после последнего запуска задания, что результат каждого выполнения задания был или просмотрите, что происходит во время выполнения задания, можно нажать ссылку в разделе «Журналы», когда вы находитесь в обзоре WebJobs: ![WebJobs диалогового окна , со стрелкой на ссылку журналы.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/18.View-All-WebJobs-and-status-of-execution.png)

Это позволит получить общие сведения о всех выполнений выбранные задания, включая /outcome состояние:

![Сведения о WebJob, включая последние задание выполняется.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/19.WebJob-Details-Overview.png)

Щелкнув выделенную ссылку, можно пойти в выполнении конкретного просмотрите журналы задания и гарантировать правильность выглядеть нормально. Это возможно, являются более качественных, если задания в действительности вызывает ошибку, и требуется проверить, что случилось, или если результата задания неправильные или не соответствует ожидаемому.

Также можно увидеть, что операторы Console.WriteLine, поэтому хорошо использованные в Мои консольного приложения для этой демонстрации теперь отображается в журнале выполнения задания:

![Сведения о WebJob, отображение строки в файл журнала.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/20.Review-Logs-and-Monitor-WebJob-Execution.png)

## <a name="tips--tricks"></a>Советы и рекомендации ##
Хотя все этого с более ранними версиями Visual Studio, сделанные все работает с помощью Visual Studio 2015. Но попутно, которые были некоторые проблемы, добавляемых их здесь в случае, если приводят к одинаковые значения.

### <a name="exit-code--2146232576-problem-when-running-the-job"></a>Выйдите из кода-2146232576 проблема при запуске задания ###
Я начала проекта Visual Studio 2015 (Предварительная версия), запуска проекта как на основании **.NET Framework 4.5.3**консольное приложение.

Локально выполнения задания работает, так как .NET Framework 4.5.3 существует на компьютере разработчика. Тем не менее после я развертывания задание для личных Windows Azure веб-сайта как WebJob сбой «**выйти из кода-2146232576**».

#### <a name="solution-make-sure-youre-on-the-correct-net-version"></a>Решение: Убедитесь, что вы находитесь на правильную версию .NET ####
Прежде чем я реализованные Azure нравится .NET Framework, версия 4.5.3, что при изменении для **.NET Framework 4.5**это работает потребовалось некоторое время.

Если приводят к эту проблему, просто убедитесь, что задание выполняется в разделе правильную версию .NET framework.
![Отображает страницу свойств проекта Visual Studio, вкладка приложения, отражающая конечного framework раскрывающегося списка, выделение точка NET Framework 4.5.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/21.Change-NET-Framework-In-Visual-Studio-2015.png)

# <a name="summary"></a>Summary #
Пока не очень большой объем к построению WebJob Azure, чтобы обеспечить их весьма сложным. Общие концепции прост очень –, но затем как со всех сложных проектов, поступающие решения для проверки подлинности, стабильность кода и надежности, сценарии высокой доступности, обслуживания и т. д. Эти переменные, уникальных для каждого проекта и следует тщательно учесть перед «только что развертывание» задание для Azure.

### <a name="related-links"></a>Ссылки по теме ###
-  Для [исходного запись в блоге на Azure WebJobs](http://zimmergren.net/technical/getting-started-with-building-azure-webjobs-timer-jobs-for-your-office-365-sites) Zimmergren Тобиаса
-  [Рекомендуемые ресурсы для Azure WebJobs](http://azure.microsoft.com/en-us/documentation/articles/websites-webjobs-resources/)
-  [Загрузить Visual Studio 2015 (Предварительная версия)](http://www.visualstudio.com/en-us/downloads/visual-studio-2015-downloads-vs.aspx)
-  [Создание надстройки SharePoint как задания таймера](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx) с Кирк Петров
-  [Процесс развертывания Azure WebJobs на веб-сайтов Azure](http://azure.microsoft.com/en-us/documentation/articles/websites-dotnet-deploy-webjobs/)
-  [Простой удаленного таймер, который взаимодействует со службой SharePoint Online](http://channel9.msdn.com/Blogs/Office-365-Dev/Simple-remote-timer-job-that-interacts-with-SharePoint-Online-Office-365-Developer-Patterns-and-Prac) с (Andrew Connell) на Channel9

### <a name="applies-to"></a>Применимо к ###
-  Office 365 нескольких клиентов (MT)
-  Office 365 выделенных (D)
-  SharePoint 2013 в локальной 
