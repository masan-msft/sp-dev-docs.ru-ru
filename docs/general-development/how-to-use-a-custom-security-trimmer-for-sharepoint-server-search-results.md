---
title: "Использование специальной фильтрации по ролям безопасности для результатов поиска в SharePoint Server"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e1a8664e-fb43-45c2-83aa-9635fe1efc99
ms.openlocfilehash: 55ea7ee4ef785f65cefe436ebe2fbc14eab4bd87
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="use-a-custom-security-trimmer-for-sharepoint-server-search-results"></a>Использование специальной фильтрации по ролям безопасности для результатов поиска в SharePoint Server

В данном практическом руководстве описывается порядок реализации — создание, развертывание и регистрация — пользовательского триммера безопасности для поиска в SharePoint с помощью Microsoft Visual Studio 2010.

Поиск в SharePoint выполняет фильтрацию по ролям безопасности время выполнения запроса из результатов поиска. Тем не менее может быть сценарии, в которых требуется выполнить фильтрацию по ролям безопасности. Поиск в SharePoint обеспечивает поддержку для следующих сценариев через ( [Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) , [Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) и [ISecurityTrimmer2](https://msdn.microsoft.com/library/Microsft.Office.Server.Search.Query.ISecurityTrimmer2.aspx) устаревшие) интерфейсов в пространстве имен [Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx) .
  
    
    

Существует два типа фильтрации по ролям безопасности: фильтрация по ролям перед и после усечения. Предварительная фильтрация по ролям относится к оценке предварительной запроса, где переопределяются запрос для добавления сведений о безопасности, перед которым сравнивается запроса в индекс поиска. После фильтрации по ролям относится к оценке после запроса, где результаты поиска, удаляются перед их возвращением для пользователя. Рекомендуется использовать предварительной фильтрации по ролям для повышения производительности и общие правильность; После фильтрации по ролям запрещает защиты от утечки информации для уточнения данных и экземпляры число попаданий.
  
    
    

Процесс регистрации триммера безопасности можно задать свойства конфигурации для настраиваемого триммера безопасности.
## <a name="overview"></a>Обзор

Фильтрация настраиваемых безопасности возможности поиска в SharePoint состоит из двух интерфейсов, которые могут использоваться для выполнения предварительной фильтрации по ролям или после обрезки результатов поиска. В данном практическом руководстве рассматриваются оба интерфейса описывающий действия, необходимые для создания и регистрации собственного триммеры безопасности.
  
    
    

## <a name="prerequisites"></a>Необходимые компоненты
<a name="PreReq"> </a>

Для выполнения этой инструкции, необходимо установить следующие компоненты в среде разработки:
  
    
    

- Поиск в Microsoft SharePoint
    
  
- Microsoft Visual Studio 2010 или аналогичную Microsoft .NET Framework - средство совместимые разработки
    
  

## <a name="set-up-a-custom-security-trimmer-project"></a>Настройка проекта настраиваемого триммера безопасности
<a name="SetUp"> </a>

На этом этапе создания проекта настраиваемого триммера безопасности и затем добавление необходимых ссылок в проект.
  
    
    

### <a name="to-create-the-project-for-a-custom-security-trimmer"></a>Создание проекта для настраиваемого триммера безопасности


1. Откройте Visual Studio и в меню **Файл** последовательно выберите элементы **Создать** и **Проект**.
    
  
2. В окне **типы проектов** перейдите в раздел **C#** выберите пункт **SharePoint**.
    
  
3. В области **Шаблоны** выберите **Пустой проект SharePoint**. В поле **имя** введите **CustomSecurityTrimmerSample** и затем нажмите кнопку **ОК**.
    
  
4. В окне **Мастер настройки SharePoint** выберите **Развернуть как решение фермы** и нажмите кнопку **Готово**.
    
  

### <a name="to-add-references-to-the-custom-security-trimmer-project"></a>Добавление ссылок в проект настраиваемого триммера безопасности


1. В меню **проект** выберите команду **Добавить ссылку**.
    
  
2. На вкладке **.NET** выберите ссылки со следующими именами компонентов и затем нажмите кнопку **ОК**:
    
  - **Компонент Microsoft Search**
    
    Вы должны увидеть две записи на вкладке **.NET** с именем компонент **компонент Microsoft Search**. Выберите запись, где столбца "путь"  это \\ISAPI\\Microsoft.Office.Server.Search.dll. При отсутствии на вкладке **.NET** в диалоговом окне **Добавление ссылок**, необходимо добавить ссылку на вкладке **Обзор**, используя путь к Microsoft.Office.Server.Search.dll.
    
  
  - **Microsoft.IdentityModel**
    
    Если на вкладке **.NET** **компонент Microsoft.IdentityModel** отсутствует, необходимо добавить ссылку на Microsoft.IdentityModel.dll на вкладке **Обзор** с помощью по следующему пути:
    
     `%ProgramFiles%\\Reference Assemblies\\Microsoft\\Windows Identity Foundation\\v4.0.`
    
  

## <a name="create-a-custom-security-pre-trimmer"></a>Создание пользовательского предварительной триммера безопасности
<a name="CreatePreTrimmer"> </a>


### <a name="to-create-the-class-file-for-the-security-pre-trimmer"></a>Чтобы создать файл класса для подготовки триммера безопасности


1. В меню **ПРОЕКТ** выберите пункт **Добавить новый элемент**.
    
  
2. В разделе **Элементы Visual C#** в разделе **Установленные шаблоны** выберите **код** и нажмите кнопку **класса**.
    
  
3. Введите **CustomSecurityPreTrimmer.cs** и нажмите кнопку **Добавить**.
    
  

### <a name="writing-the-custom-security-pre-trimmer-code"></a>Написание кода предварительной фильтрации по ролям безопасности

Ваше настраиваемого триммера безопасности необходимо реализовать интерфейс **ISecurityTrimmerPre**. В следующем примере кода  это базовая реализацию этого интерфейса.
  
    
    

### <a name="to-modify-the-default-code-in-customsecuritypretrimmer"></a>Изменение кода по умолчанию в CustomSecurityPreTrimmer


1. Добавьте в начало класса следующие директивы **using**.
    
```cs
  
using System;
using System.Collections;
using System.Collections.Generic;
using System.Collections.Specialized;
using System.Security.Principal;
using Microsoft.IdentityModel.Claims;
using Microsoft.Office.Server.Search.Query;
using Microsoft.Office.Server.Search.Administration;

```

2. Укажите, что класс **CustomSecurityPreTrimmer** реализует интерфейс [ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) в объявлении класса, как показано в следующем коде.
    
```cs
  
public class CustomSecurityPreTrimmer : ISecurityTrimmerPre
```


### <a name="to-implement-the-isecuritytrimmerpre-interface-methods"></a>Реализация методов интерфейса ISecurityTrimmerPre


1. Добавьте следующий код для объявления метода  [Initialize()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.Initialize.aspx) .
    
```cs
  public void Initialize(NameValueCollection staticProperties, SearchServiceApplication searchApplication)
{

}
```


    The basic version of this sample does not include any code in the **Initialize** method.
    
  
2. Добавьте следующий код для объявления метода  [AddAccess()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.AddAccess.aspx) .
    
```cs
  
public IEnumerable<Tuple<Claim, bool>> AddAccess(
                IDictionary<string, object> sessionProperties, IIdentity passedUserIdentity)
{
//AddAccess method implementation, see steps 3-5.
}
```

3. В первой части реализации метода **AddAccess** Узнайте пользователей, которые пользователь является, посмотрев _passedUserIdentity_.
    
```cs
  
if (passedUserIdentity == null)
{
   throw new ArgumentException("AddAccess method is called with invalid user identity
   parameter", "passedUserIdentity");
}
            
   String strUser = null;
   var claimsIdentity = (IClaimsIdentity)passedUserIdentity;
   if (claimsIdentity != null)
   {
      foreach (var claim in claimsIdentity.Claims)
      {
         if (claim == null) 
         {
            continue;
         }
         
         // strUser is "domain\\\\user" format when web app is in Claims Windows Mode
         if (SPClaimTypes.Equals(claim.ClaimType, SPClaimTypes.UserLogonName))
         {
            strUser = claim.Value;
            break;
         }

         // strUser2 is "S-1-5-21-2127521184-1604012920-1887927527-66602" when web app is   
            in Legacy Windows Mode
         // In this case we need to convert it into NT user format.
         if (SPClaimTypes.Equals(claim.ClaimType, ClaimTypes.PrimarySid))
         {
            strUser = claim.Value;
            SecurityIdentifier sid = new SecurityIdentifier(strUser);
            strUser = sid.Translate(typeof(NTAccount)).Value;
            break;
         }
      }
}            

```

4. Создание списка, в списке с помощью утверждений и возврата списка, как показано в следующем коде.
    
```cs
  
var claims = new LinkedList<Tuple<Claim, bool>>();
if (!string.IsNullOrEmpty(strUser))
   {
      var groupMembership = GetMembership(strUser);
      if (!string.IsNullOrEmpty(groupMembership))
      {
         var groups = groupMembership.Split(new[] {';'},
         StringSplitOptions.RemoveEmptyEntries);
         foreach (var group in groups)
         {
            claims.AddLast(new Tuple<Claim, bool>(
            new Claim("http://schemas.happy.bdc.microsoft.com/claims/acl", group), false));
         }
      }
   }
   return claims;
}

```


    The **GetMembership** method contains the custom logic of your trimmer.
    
  

## <a name="create-a-custom-security-post-trimmer"></a>Создание пользовательского после триммера безопасности
<a name="CreatePostTrimmer"> </a>


### <a name="to-create-the-class-file-for-the-security-post-trimmer"></a>Чтобы создать файл класса для триммера безопасности после завершения


1. В меню **ПРОЕКТ** выберите пункт **Добавить новый элемент**.
    
  
2. В разделе **Элементы Visual C#** в разделе **Установленные шаблоны** выберите **код**, а затем выберите **класс**...
    
  
3. Введите CustomSecurityPostTrimmer.csи нажмите кнопку **Добавить**.
    
  

### <a name="writing-the-custom-security-post-trimmer-code"></a>Написание кода после фильтрации по ролям безопасности

Ваше настраиваемого триммера безопасности необходимо реализовать интерфейс **ISecurityTrimmerPost**. В примере кода в этом разделе представлена базовая реализацию этого интерфейса.
  
    
    

### <a name="to-modify-the-default-code-in-customsecurityposttrimmer"></a>Изменение кода по умолчанию в CustomSecurityPostTrimmer


1. Добавьте в начало класса следующие директивы **using**.
    
```cs
  
using System;
using System.Collections;
using System.Collections.Generic;
using System.Collections.Specialized;
using System.Security.Principal;
using Microsoft.IdentityModel.Claims;
using Microsoft.Office.Server.Search.Query;
using Microsoft.Office.Server.Search.Administration;

```

2. Укажите, что класс **CustomSecurityPostTrimmer** реализует интерфейс [ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) в объявлении класса следующим образом:
    
```cs
  
public class CustomSecurityPostTrimmer : ISecurityTrimmerPost
```


### <a name="to-implement-the-isecuritytrimmerpost-interface-methods"></a>Реализация методов интерфейса ISecurityTrimmerPost


1. Добавьте следующий код для объявления метода  [Initialize()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.Initialize.aspx) .
    
```cs
  public void Initialize(NameValueCollection staticProperties, SearchServiceApplication searchApplication)
{

}
```


    The basic version of this sample does not include any code in the Initialize method.
    
  
2. Добавьте следующий код для объявления метода  [CheckAccess()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.CheckAccess.aspx) .
    
```cs
  
public BitArray CheckAccess(IList<string> documentCrawlUrls, IList<string> documentAcls, IDictionary<string, object> sessionProperties, IIdentity passedUserIdentity)
{
//CheckAccess method implementation, see steps 3-5.
}
```

3. Первая часть реализации метода **CheckAccess** объявить и инициализировать переменную **BitArray** для хранения результатов проверки доступа для каждого URL-адреса в коллекции **documentCrawlUrls** и извлечения пользователя, который отправил запрос, как показано в следующем коде.
    
```cs
  
if (documentCrawlUrls == null)
{
   throw new ArgumentException("CheckAccess method is called with invalid URL list",
   "documentCrawlUrls");
}
if (documentAcls == null)
{
   throw new ArgumentException("CheckAccess method is called with invalid documentAcls   
   list", "documentAcls");
}
if (passedUserIdentity == null)
{
   throw new ArgumentException("CheckAccess method is called with invalid user identity
   parameter", "passedUserIdentity");
}

```

4. Пройдитесь по каждой URL-адрес обхода в коллекции и выполните проверку доступа, чтобы определить, если пользователь, отправивший запрос можно получить доступ к URL-адрес обхода связанного элемента контента, как показано в следующем коде. 
    
```cs
  
// Initialize the bit array with TRUE value which means all results are visible by default.
var urlStatusArray = new BitArray(documentCrawlUrls.Count, true);
var claimsIdentity = (IClaimsIdentity)passedUserIdentity;
if (claimsIdentity != null)
{
   var userGroups = GetGroupList(claimsIdentity.Claims);
   var numberDocs = documentCrawlUrls.Count;
   for (var i = 0; i < numberDocs; ++i)
   {
      if (!string.IsNullOrEmpty(documentAcls[i]))
      {
         urlStatusArray[i] = VerifyAccess(documentAcls[i], userGroups);
      }
   }
}

```


    If the user has access to the content item, set the value of the **BitArray** item at that index, **urlStatusArray[i]**, to **true**; otherwise, set it to **false**.
    
  
5. Значение возвращаемое значение метода **CheckAccess** **urlStatusArray**, как показано в следующем коде.
    
```cs
  
return urlStatusArray;
```


## <a name="register-the-custom-security-trimmer"></a>Зарегистрируйте пользовательский триммер безопасности.
<a name="RegisterTrimmer"> </a>

Этот шаг описывается настройка настраиваемого триммера безопасности и включает в себя следующие задачи:
  
    
    

- Регистрация настраиваемого триммера безопасности для приложения службы поиска с помощью командлетов Windows PowerShell.
    
  
- Перезапуск SharePoint хост-контроллер поиска (SPSearchHostController).
    
  

### <a name="register-the-custom-security-trimmer"></a>Зарегистрируйте пользовательский триммер безопасности.

Используйте Командная консоль SharePoint для регистрации настраиваемого триммера безопасности в  _ClassName_. В нашем случае  _ClassName_ может быть **CustomSecurityPreTrimmer** или **CustomSecurityPostTrimmer**. В следующей процедуре показано, как зарегистрировать пользовательский триммер безопасности, с Идентификатором, равным 1 для приложения службы поиска.
  
    
    

### <a name="to-register-the-custom-security-trimmer"></a>Регистрация настраиваемого триммера безопасности


1. В проводнике найдите файл CustomSecurityTrimmerSample.dll, расположенный в каталоге  _<Local_Drive>_:\\WINDOWS\\assembly.
    
  
2. Откройте контекстное меню для файла и выберите пункт Свойства.
    
  
3. На вкладке **Общие** диалогового окна **Свойства** выберите и скопируйте маркер.
    
  
4. Откройте Командная консоль SharePoint. Сведения об использовании этого средства можно  [Администрирование приложений-служб с помощью консоли управления SharePoint 2010](http://msdn.microsoft.com/library/aff64855-7377-4e4a-b3a9-b620c9047076%28Office.15%29.aspx)
    
  
5. Введите в командной строке следующую команду.
    
```
  New-SPEnterpriseSearchSecurityTrimmer -SearchApplication "Search Service Application"
-typeName "CustomSecurityTrimmerSample.ClassName, CustomSecurityTrimmerSample, 
Version=1.0.0.0, Culture=neutral, PublicKeyToken=token" -RulePath "xmldoc://*"
```


    In the command, replace  _ClassName_ either with **CustomSecurityPreTrimmer** or **CustomSecurityPostTrimmer** and _token_ with the Public Key Token for the CustomSecurityTrimmerSample.dll file. You must associate all post-trimmers with a crawl rule, _"xmldoc://*"_; but this is optional for pre-trimmers.
    
    > [!NOTE]
    > If you have multiple front-end web servers, you must deploy your security trimmer to the global assembly cache on all the front-end web servers in the farm. 

6. Убедитесь, что следующие командлеты PowerShell зарегистрирован триммер безопасности.
    
```
  
$searchApp = Get-SPEnterpriseSearchServiceApplication
$searchApp | Get-SPEnterpriseSearchSecurityTrimmer
```


    Your security trimmer must be visible in the results.
    
  

### <a name="to-restart-the-sharepoint-search-host-controller"></a>Чтобы перезапустить хост-контроллер поиска SharePoint


- Можно перезапустить службу поиска, введя следующий командлет PowerShell.
    
```
  
net restart sphostcontrollerservice

```


## <a name="see-also"></a>См. также
<a name="bk_sectrimmer_addlresources"> </a>


-  [Специальная фильтрация по ролям безопасности, настраиваемая для поиска в SharePoint](custom-security-trimming-for-search-in-sharepoint-server.md)
    
  
-  [Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx)
    
  
-  [Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx)
    
  
-  [Microsoft.Office.Server.Search.Query.PluggableAccessCheckException](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.PluggableAccessCheckException.aspx)
    
  

