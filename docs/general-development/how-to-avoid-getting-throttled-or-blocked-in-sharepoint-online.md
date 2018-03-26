---
title: Как избежать регулирования или блокировки в SharePoint Online
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 33ed8106-d850-42b1-8d7f-5ba83901149c
ms.openlocfilehash: 6f0caad2181e78a2f60ee82bd4434aeb203a5395
ms.sourcegitcommit: adfe402a7646c7061288aa6669442ae03598175a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/23/2018
---
# <a name="avoid-getting-throttled-or-blocked-in-sharepoint-online"></a>Как избежать регулирования или блокировки в SharePoint Online
Узнайте о регулирования в SharePoint Online и узнайте, как избежать регулирование или заблокирован. Включает пример кода CSOM и REST, которые можно использовать для упрощения задачи.

-  [Что такое регулирование?](how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online.md#BKMK_Whatisthrottling)

-  [Общие сценарии регулирования в SharePoint Online](how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online.md#BKMK_Commonthrottlingscenarios)

-  [Почему не удается вы только что Расскажите мне точное ограничения полосы пропускания?](how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online.md#BKMK_Whycantyoujusttellmetheexactthrottlinglimits)

-  [Рекомендации по обработке регулирования](how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online.md#BKMK_Bestpracticestohandlethrottling)
    
- [Как для оформления трафик во избежание получения регулирование?](how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online.md#BKMK_DecorateSharePointOnlineThrottling)
  
-  [Примеры кода репозиториев CSOM: SharePoint Online регулирования](how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online.md#BKMK_GitHubCSOMandRESTcodesamplesSharePointOnlineThrottling)
    
  
-  [Что делать, если блокируются в SharePoint Online ?](how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online.md#BKMK_Whatshouldyoudoifyougetblocked)
    
  
-  [Дополнительные ресурсы](how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online.md#BKMK_Additionalresources)

Не похоже на этом? Трассировка запускается процесс CSOM  например, для переноса файлов в SharePoint Online -, но оставьте начало регулирование. Или более того, вы получите полностью заблокировано. Что происходит и что можно сделать, чтобы сделать его остановить?
  
## <a name="what-is-throttling"></a>Что такое регулирование?
<a name="BKMK_Whatisthrottling"> </a>

для обеспечения оптимальной производительности и надежности службы SharePoint OnlineSharePoint Online использует регулирования. Пределы регулирования количество пользовательских действий или одновременных звонков (с скриптах или программах) для предотвращения чрезмерного использования ресурсов.
  
С другой стороны, очень редко пользователю получить ограничением в SharePoint Online. Службу надежную, и он предназначен для обработки очень большой поток. Если вы получите ограничением, 99% времени его из-за пользовательского кода. Это не означает, что не другие способы получения ограничением, только что они являются реже. Например включается 10 машины и иметь клиент синхронизации, перейдя на все 10. На каждом синхронизируйте 1 ТБ содержимого. Это получили бы вы регулирование.
  

![Как происходит регулирование](../images/3b9184db-99a4-416e-ba1e-7f8653484cee.png)
  
### <a name="what-happens-when-you-get-throttled-in-sharepoint-online"></a>Что происходит при получения ограничением в SharePoint Online ?

Когда пользователь превышает ограничения на использование, SharePoint Online регулировки все последующие запросы из этой учетной записи пользователя в течение короткого периода. Все действия пользователя подвергаются регулированию время повтора.
  
- Для запросов, которые пользователь должен выполнить непосредственно в браузере SharePoint Online перенаправляет пользователя на страницу регулирования сведения и запросы завершиться с ошибкой.
  
- Для всех остальных запросах, включая вызовы REST или CSOM, SharePoint Online возвращает код состояния HTTP 429 ("слишком много запросов"), и запросы завершиться с ошибкой.
  
Если процесс оскорбительного продолжает превышает ограничения на использование, SharePoint Online может полностью заблокировать процесса; в этом случае может появиться код состояния HTTP 503 ("Служба недоступна"), и мы будем напоминания о том, блокировки в центре сообщений Office 365. Ниже показан сообщение об ошибке.
      
![Сообщение об ошибке 503: сервер недоступен](../images/e70a43c1-43ba-4f5c-b25f-e3995f18dd16.png)
      
503 Сервер недоступен, сообщение.

## <a name="common-throttling-scenarios-in-sharepoint-online"></a>Общие сценарии регулирования в SharePoint Online
<a name="BKMK_Commonthrottlingscenarios"> </a>

Самые распространенные причины регулирования в SharePoint Online пользователей являются клиентской объектной модели (CSOM) или представлений состояния (REST) кода, который выполняет слишком много действий слишком часто.
    

- **Случайные трафика**
    
    Не достаточно трафика в любой момент времени, но достаточно со временем, на котором запущен и выходить из нее, регулирование эпизодическое образом.
    
  - Например, после перенос файлов SharePoint Online, можно запустить настраиваемый скрипт REST или CSOM обновление метаданных на файлы. Сценарий CSOM/REST выполняется обновление большое число файлов в очень высокая частота, который запускает регулирования. Аналогично графического пользовательского интерфейса автозаполнения, с помощью службы REST, выполнение слишком большого числа вызовов в списки во время работы каждого конечного пользователя, может вызвать появление регулирования, в зависимости от того, какие другие операции занимающих ресурсы в то же время.
    
  ![Разовое регулирование](../images/a61afe25-9597-403f-b3fa-d3f630155021.png)
  
- **Много избыточных элементов трафика**
    
    Один процесс значительно превышает регулирования ограничения постоянно, в течение длительного времени.
    
  - Веб-службы используются для формирования средство для синхронизации свойств профиля пользователя. Средство обновляет свойства профиля пользователя на основе сведений из бизнес-системы отдела кадров (HR) (LOB). Средство выполняет вызовы в слишком высокая частота.
  
  - Запуске сценария нагрузочного тестирования на SharePoint Online и получение регулирование. Не допускается SharePoint Online нагрузочного тестирования.
  
  - Настроить сайта группы на SharePoint Online, например, путем добавления индикатор состояния на домашней странице. Этот индикатор состояния обновляет часто, которая приводит к слишком большого числа звонков в службу SharePoint Online страницы  это инициирующую регулирования.
    
  ![Стабильное регулирование](../images/7849d413-381f-4558-9e50-b3cc9990d3e3.png)
  
## <a name="why-cant-you-just-tell-me-the-exact-throttling-limits"></a>Почему не удается вы только что Расскажите мне точное ограничения полосы пропускания?
<a name="BKMK_Whycantyoujusttellmetheexactthrottlinglimits"> </a>

Настройка и публикация точное регулирование ограничивает очень просто звуки, но на самом деле это не лучший способ перехода. Мы постоянно отслеживать использование ресурсов на SharePoint Online. В зависимости от использования мы точной пороговые значения, поэтому пользователи могут использовать максимальное количество ресурсов без снижения надежности и производительности SharePoint Online. Вот почему это важно для вашего кода CSOM или REST для включения добавочного назад для обработки регулирования; Это позволяет максимально быстро запуск каждый день кода и пассивный режим «только что достаточно» позволяет коду, если достигает ограничения полосы пропускания. Примеры кода далее в этой статье показано, как использовать добавочного пассивный режим.

## <a name="best-practices-to-handle-throttling"></a>Рекомендации по обработке регулирования
<a name="BKMK_Bestpracticestohandlethrottling"> </a>

- Уменьшите количество операций в запросе
    
- Уменьшить частоту звонков
    
- Оформление трафика, поэтому мы знаем, которые (в разделе на трафик оформления рекомендация Подробнее об этом ниже)
    
При выполнении в регулирования, мы рекомендуем добавочного пассивный режим для уменьшения числа и частота вызовов до более регулировка отсутствует.

Между повторными попытками перед повторением для выполнения кода, который был регулирование ожидает добавочного пассивный использует постепенно больше времени. Примеры кода репозиториев, можно использовать далее в этой статье, записываются как методы расширения для добавления добавочного назад код.
    
Резервное является быстрым способом для обработки ограничением, так как SharePoint Online по-прежнему производится для записи в журнал использования ресурсов во время применяется регулирование пользователя. Другими словами агрессивные повторных попыток работать в вы, потому что несмотря на то, что вызовы с ошибкой, они по-прежнему улучшаются от ограничения на использование. Быстрее пассивный режим, тем быстрее будет остановлено, превышающие ограничения на использование. 

For information about ways to monitor your SharePoint Online activity, see  [Diagnosing performance issues with SharePoint Online](https://support.office.com/en-us/article/3c364f9e-b9f6-4da4-a792-c8e8c8cd2e86).

For a broader discussion of throttling on the Microsoft Cloud, see  [Throttling Pattern](http://msdn.microsoft.com/library/4baf5af2-32fc-47ab-8569-3e5c59a5ebd5.aspx).

## <a name="how-to-decorate-your-http-traffic-to-avoid-throttling"></a>Как для оформления http-трафика во избежание регулирование?
<a name="BKMK_DecorateSharePointOnlineThrottling"> </a>

Для обеспечения высокого уровня доступности, может регулирование некоторых трафика. Регулирование происходит при работоспособности системы — речь, а одно из условий, используемые для регулирования — оформления трафика, который влияет на непосредственно на определение приоритетов трафика. Также внутреннего трафика приоритетов через трафика, который не параметризованные должным образом.
 
Что такое определение упрощенного трафика?

- Трафик упрощенного, если строка не AppID/AppTitle или агент пользователя в вызове API-Интерфейс REST или CSOM к SharePoint Online.

Какие существуют рекомендации?

- При создании приложения, рекомендуется зарегистрировать и использовать AppID и AppTitle — это обеспечит наиболее возможности различных клиентов и наиболее путь для любого решения будущих проблем. Также включать данные строка агента пользователя как определено в следующем шаге.

- Необходимо указать строка агента пользователя при вызове API SharePoint с помощью следующих соглашение об именовании

| Тип  | Агент пользователя  | Описание   |
|---|---|---|
| Приложения независимых поставщиков программных Продуктов | Независимых поставщиков программных Продуктов & #124; CompanyName & #124; AppName и версии | Определить в качестве независимых поставщиков программных Продуктов и включать название компании, имя приложения, разделенных символом конвейеризации, а затем добавляя номер версии, разделенных точкой с косой черты  |
| Корпоративного приложения | NONISV & #124; CompanyName & #124; AppName и версии | Определить в качестве NONISV и включать название компании, имя приложения, разделенных символом конвейеризации, а затем добавляя номер версии, разделенных точкой с косой черты |

- При создании собственного библиотеки JavaScript, которые используются для вызова API-интерфейсов SharePoint Online, убедитесь в том, включают сведения агента пользователя http-запрос и потенциально Регистрация веб-приложения также как приложение, где подходящее.

> [!NOTE]
> Формат строка агента пользователя ожидается выполните [RFC2616](http://www.ietf.org/rfc/rfc2616.txt), так что произведите выполните копирование выше рекомендации на правом разделителей. Также дает возможность добавлять существующие строка агента пользователя с запрошенные данные.

> [!NOTE]
> При разработке компонентов переднего плана выполнения в браузере, большинство современных браузеров не разрешать overwritting строка агента пользователя и не требуется реализовать ее.

### <a name="example-of-decorating-traffic-with-user-agent-when-using-client-side-object-model-csom"></a>Пример оформления трафика с помощью агента пользователя, при использовании модели объектов со стороны клиента (CSOM)

```cs
// Get access to source site
using (var ctx = new ClientContext("https://contoso.sharepoint.com/sites/team"))
{
    //Provide account and pwd for connecting to SharePoint Online
    var passWord = new SecureString();
    foreach (char c in pwd.ToCharArray()) passWord.AppendChar(c);
    ctx.Credentials = new SharePointOnlineCredentials("contoso@contoso.onmicrosoft.com", passWord);

    // Add our User Agent information
    ctx.ExecutingWebRequest += delegate (object sender, WebRequestEventArgs e)
    {
        e.WebRequestExecutor.WebRequest.UserAgent = "NONISV|Contoso|GovernanceCheck/1.0";
    };
                
    // Normal CSOM Call with custom User-Agent information
    Web site = ctx.Web;
    ctx.Load(site);
    ctx.ExecuteQuery();
}
```

### <a name="example-of-decorating-traffic-with-user-agent-when-using-rest-apis"></a>Пример оформления трафика с помощью агента пользователя, при использовании API-интерфейсы REST

Следующий пример является форматом c#, но аналогичные сведения агента пользователя, рекомендуется использовать даже для библиотеки JavaScript, используемые на страницах SharePoint Online.

```cs
HttpWebRequest endpointRequest = (HttpWebRequest)HttpWebRequest.Create(sharepointUrl.ToString() + "/_api/web/lists");
endpointRequest.Method = "GET";
endpointRequest.UserAgent = "NONISV|Contoso|GovernanceCheck/1.0";
endpointRequest.Accept = "application/json;odata=verbose";
endpointRequest.Headers.Add("Authorization", "Bearer " + accessToken);
HttpWebResponse endpointResponse = (HttpWebResponse)endpointRequest.GetResponse();
```


## <a name="github-csom-code-samples-sharepoint-online-throttling"></a>Примеры кода репозиториев CSOM: SharePoint Online регулирования
<a name="BKMK_GitHubCSOMandRESTcodesamplesSharePointOnlineThrottling"> </a>

 [CoreThrottling](https://github.com/OfficeDev/PnP/tree/dev/Samples/Core.Throttling) в [Office 365 для разработчиков шаблонов и рекомендациям репозитория ](http://github.com/OfficeDev/PnP) приведен пример кода, в котором показывается добавочного пассивный метод. Эта технология требует минимальной изменений в коде.
  
    
    
Прежде чем запускать этот пример кода:
  
    
    

- Откройте **файл Program.cs** и введите следующие сведения в **методе**:
    
  - Учетные данные учетной записи разработчика Office 365.
    
  
  - URL-адрес вашего сайта разработчика Office 365.
    
  
  - Имя тестовой библиотеке документов на вашем сайте разработчика Office 365.
    
  
- В случае об ошибке, указывающее, является недопустимым, что файл **App.Config**, перейдите в **Окне Обозреватель решений** щелкните правой кнопкой мыши **файл App.config** и выберите команду **Исключить из проекта**.
    
  
 **Core.Throttling** работает как консольное приложение, с помощью политики авторизации только для пользователя, которая означает, что в этом примере кода используется разрешения текущего пользователя. В методе **Main** в файле Program.cs цикла while повторно создает вложенные папки в библиотеке документов, тестирования. Затем вызов **ctx. ExecuteQueryWithExponentialRetry**, который использует CSOM для выполнения метода **ExecuteQuery**. **ExecuteQueryWithExponentialRetry**  это метод расширения на объект [ClientContext](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.clientcontext%28v=office.15%29.aspx) и определены в **ClientContextExtension.cs**.
  

Если SharePoint Online регулировки оператор **ExecuteQuery**, **ExecuteQueryWithIncrementalRetry** запускает добавочного пассивный метод с:

- Перехват **веб-исключение** и проверке **HttpWebResponse.StatusCode**. Если SharePoint Online регулирование оператор **ExecuteQuery**, **HttpWebResponse.StatusCode**  429.

- Текущий поток приостанавливается для периода, указанного в **backoffInterval**.

- При возобновлении текущего потока **backoffInterval** удваивается и увеличивается количество повторных попыток выполнить ( **retryAttempts** ). С удвоения **backoffInterval** кода приостанавливается активности на длительный период времени перед повторным выполнением кода, который был применяется регулирование SharePoint Online.

- Процесс повторяется до оператора **ExecuteQuery** выполнена успешно, либо превысила число разрешенных повторов ( **retryCount** ).

### <a name="csom-code-sample-incremental-back-off-and-retry-calls-executequerywithincrementalretry-method-later-in-this-article"></a>Пример кода CSOM: добавочного пассивный и повторите попытку (вызывает метод ExecuteQueryWithIncrementalRetry далее в этой статье)

```

using (var ctx = new ClientContext(serverUrl))
       {
           //Provide account and pwd for connecting to the source
           var passWord = new SecureString();
           foreach (char c in password.ToCharArray()) passWord.AppendChar(c);
           ctx.Credentials = new SharePointOnlineCredentials(login, passWord);
            try
           {
               int number = 0;
               // This loop will be executed 1000 times, which will cause throttling to occur
               while (number < 1000)
               {
                   // Try to create new folder based on Ticks to the given list as an example process
                   var folder = ctx.Site.RootWeb.GetFolderByServerRelativeUrl(listUrlName);
                   ctx.Load(folder);
                   folder = folder.Folders.Add(DateTime.Now.Ticks.ToString());
                   // Extension method for executing query with throttling checks
                   ctx.ExecuteQueryWithIncrementalRetry(5, 30000); //5 retries, with a base delay of 30 secs.
                   // Status indication for execution.
                   Console.WriteLine("CSOM request successful.");
                   // For loop handling.
                   number = number + 1;
               }
           }
           catch (MaximumRetryAttemptedException mex)
           {
               // Exception handling for the Maximum Retry Attempted
               Console.WriteLine(mex.Message);
           }
       }

```


### <a name="csom-code-sample-executequerywithincrementalretry-method"></a>Пример кода CSOM: метод ExecuteQueryWithIncrementalRetry


```

public static void ExecuteQueryWithIncrementalRetry(this ClientContext context, int retryCount, int delay)
        {
            int retryAttempts = 0;
            int backoffInterval = delay;
            if (retryCount <= 0)
                throw new ArgumentException("Provide a retry count greater than zero.");
           if (delay <= 0)
                throw new ArgumentException("Provide a delay greater than zero.");
           while (retryAttempts < retryCount)
            {
                try
                {
                    context.ExecuteQuery();
                    return;
                }
                catch (WebException wex)
                {
                    var response = wex.Response as HttpWebResponse;
                    if (response != null &amp;&amp; response.StatusCode == (HttpStatusCode)429)
                    {
                        Console.WriteLine(string.Format("CSOM request exceeded usage limits. Sleeping for {0} seconds before retrying.", backoffInterval));
                        //Add delay.
                        System.Threading.Thread.Sleep(backoffInterval);
                        //Add to retry count and increase delay.
                        retryAttempts++;
                        backoffInterval = backoffInterval * 2;
                    }
                    else
                    {
                        throw;
                    }
                }
            }
            throw new MaximumRetryAttemptedException(string.Format("Maximum retry attempts {0}, have been attempted.", retryCount));
       }

```


## <a name="what-should-you-do-if-you-get-blocked-in-sharepoint-online"></a>Что делать, если блокируются в SharePoint Online ?
<a name="BKMK_Whatshouldyoudoifyougetblocked"> </a>

Блокировка  большой формы регулирования. Мы редко никогда не блокировать клиента, пока мы определим долгосрочного, очень чрезмерное количество трафика, которые может нарушить общее состояние службы SharePoint Online. Мы применить блоки для предотвращения снижения производительности и надежности SharePoint Online большой трафик. Блок - которого обычно размещается на уровне клиента  запрещает оскорбительного процесс до решить проблему. Если мы заблокировать подписки, необходимо выполнить действие, которое необходимо изменить оскорбительного процессов перед удалением блока.
  
Если мы заблокировать подписки, вы увидите код состояния HTTP 503, и мы будем напоминания о том, блокировки в центре сообщений Office 365. Сообщение описывает причину блокировки, представлены рекомендации о том, как устранить проблему, вызвавшей ошибку и вы узнаете, к кому обращаться для получения блока удалены.
  
## <a name="see-also"></a>См. также
<a name="BKMK_Additionalresources"> </a>

-  [Diagnosing performance issues with SharePoint Online](https://support.office.com/en-us/article/3c364f9e-b9f6-4da4-a792-c8e8c8cd2e86)
  
-  [Capacity planning and load testing SharePoint Online](http://msdn.microsoft.com/library/22fa7e7e-7554-4987-b56f-b39bbf303a0a.aspx)
  
-  [GitHub: Пример кода для регулирования SharePoint Online](https://github.com/OfficeDev/PnP/tree/dev/Samples/Core.Throttling)
