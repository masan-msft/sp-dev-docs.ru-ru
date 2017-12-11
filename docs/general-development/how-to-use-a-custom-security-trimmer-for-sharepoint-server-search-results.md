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
# <a name="use-a-custom-security-trimmer-for-sharepoint-server-search-results"></a><span data-ttu-id="c9496-102">Использование специальной фильтрации по ролям безопасности для результатов поиска в SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="c9496-102">Use a custom security trimmer for SharePoint Server search results</span></span>

<span data-ttu-id="c9496-103">В данном практическом руководстве описывается порядок реализации — создание, развертывание и регистрация — пользовательского триммера безопасности для поиска в SharePoint с помощью Microsoft Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="c9496-103">This how-to guides you through the steps to implement—create, deploy, and register—a custom security trimmer for Search in SharePoint by using Microsoft Visual Studio 2010.</span></span>

<span data-ttu-id="c9496-104">Поиск в SharePoint выполняет фильтрацию по ролям безопасности время выполнения запроса из результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="c9496-104">Search in SharePoint performs query-time security trimming of search results.</span></span> <span data-ttu-id="c9496-105">Тем не менее может быть сценарии, в которых требуется выполнить фильтрацию по ролям безопасности.</span><span class="sxs-lookup"><span data-stu-id="c9496-105">However, there may be scenarios in which you want to perform custom security trimming.</span></span> <span data-ttu-id="c9496-106">Поиск в SharePoint обеспечивает поддержку для следующих сценариев через ( [Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) , [Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) и [ISecurityTrimmer2](https://msdn.microsoft.com/library/Microsft.Office.Server.Search.Query.ISecurityTrimmer2.aspx) устаревшие) интерфейсов в пространстве имен [Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c9496-106">Search in SharePoint provides support for these scenarios through the  [Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) , [Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) , and [ISecurityTrimmer2](https://msdn.microsoft.com/library/Microsft.Office.Server.Search.Query.ISecurityTrimmer2.aspx) (deprecated) interfaces in the [Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx) namespace.</span></span>
  
    
    

<span data-ttu-id="c9496-p102">Существует два типа фильтрации по ролям безопасности: фильтрация по ролям перед и после усечения. Предварительная фильтрация по ролям относится к оценке предварительной запроса, где переопределяются запрос для добавления сведений о безопасности, перед которым сравнивается запроса в индекс поиска. После фильтрации по ролям относится к оценке после запроса, где результаты поиска, удаляются перед их возвращением для пользователя. Рекомендуется использовать предварительной фильтрации по ролям для повышения производительности и общие правильность; После фильтрации по ролям запрещает защиты от утечки информации для уточнения данных и экземпляры число попаданий.</span><span class="sxs-lookup"><span data-stu-id="c9496-p102">There are two kinds of custom security trimming: Pre-trimming and post-trimming. Pre-trimming refers to pre-query evaluation where the query is rewritten to add security information before the query is matched to the search index. Post-trimming refers to post-query evaluation where the search results are pruned before they are returned to the user. We recommend the use of pre-trimming for performance and general correctness; post-trimming prevents information leakage for refiner data and hit count instances.</span></span>
  
    
    

<span data-ttu-id="c9496-111">Процесс регистрации триммера безопасности можно задать свойства конфигурации для настраиваемого триммера безопасности.</span><span class="sxs-lookup"><span data-stu-id="c9496-111">The security trimmer registration process enables you to specify configuration properties for the custom security trimmer.</span></span>
## <a name="overview"></a><span data-ttu-id="c9496-112">Обзор</span><span class="sxs-lookup"><span data-stu-id="c9496-112">Overview</span></span>

<span data-ttu-id="c9496-113">Фильтрация настраиваемых безопасности возможности поиска в SharePoint состоит из двух интерфейсов, которые могут использоваться для выполнения предварительной фильтрации по ролям или после обрезки результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="c9496-113">Custom Security Trimming in Search in SharePoint consists of two interfaces that can be used to carry out pre-trimming or post-trimming of your search results.</span></span> <span data-ttu-id="c9496-114">В данном практическом руководстве рассматриваются оба интерфейса описывающий действия, необходимые для создания и регистрации собственного триммеры безопасности.</span><span class="sxs-lookup"><span data-stu-id="c9496-114">This how-to focuses on both interfaces, describing the steps necessary to create and register your own security trimmers.</span></span>
  
    
    

## <a name="prerequisites"></a><span data-ttu-id="c9496-115">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="c9496-115">Prerequisites</span></span>
<span data-ttu-id="c9496-116"><a name="PreReq"> </a></span><span class="sxs-lookup"><span data-stu-id="c9496-116"><a name="PreReq"> </a></span></span>

<span data-ttu-id="c9496-117">Для выполнения этой инструкции, необходимо установить следующие компоненты в среде разработки:</span><span class="sxs-lookup"><span data-stu-id="c9496-117">To complete this how-to, you must have the following installed in your development environment:</span></span>
  
    
    

- <span data-ttu-id="c9496-118">Поиск в Microsoft SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9496-118">Search in Microsoft SharePoint</span></span>
    
  
- <span data-ttu-id="c9496-119">Microsoft Visual Studio 2010 или аналогичную Microsoft .NET Framework - средство совместимые разработки</span><span class="sxs-lookup"><span data-stu-id="c9496-119">Microsoft Visual Studio 2010 or similar Microsoft .NET Framework-compatible development tool</span></span>
    
  

## <a name="set-up-a-custom-security-trimmer-project"></a><span data-ttu-id="c9496-120">Настройка проекта настраиваемого триммера безопасности</span><span class="sxs-lookup"><span data-stu-id="c9496-120">Set up a custom security trimmer project</span></span>
<span data-ttu-id="c9496-121"><a name="SetUp"> </a></span><span class="sxs-lookup"><span data-stu-id="c9496-121"><a name="SetUp"> </a></span></span>

<span data-ttu-id="c9496-122">На этом этапе создания проекта настраиваемого триммера безопасности и затем добавление необходимых ссылок в проект.</span><span class="sxs-lookup"><span data-stu-id="c9496-122">In this step, you will create the custom security trimmer project, and then add the required references to the project.</span></span>
  
    
    

### <a name="to-create-the-project-for-a-custom-security-trimmer"></a><span data-ttu-id="c9496-123">Создание проекта для настраиваемого триммера безопасности</span><span class="sxs-lookup"><span data-stu-id="c9496-123">To create the project for a custom security trimmer</span></span>


1. <span data-ttu-id="c9496-124">Откройте Visual Studio и в меню **Файл** последовательно выберите элементы **Создать** и **Проект**.</span><span class="sxs-lookup"><span data-stu-id="c9496-124">Open Visual Studio and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="c9496-125">В окне **типы проектов** перейдите в раздел **C#** выберите пункт **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="c9496-125">In **Project types**, under **C#**, choose **SharePoint**.</span></span>
    
  
3. <span data-ttu-id="c9496-p104">В области **Шаблоны** выберите **Пустой проект SharePoint**. В поле **имя** введите **CustomSecurityTrimmerSample** и затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c9496-p104">Under **Templates**, choose **Empty SharePoint Project**. In the **Name** field, type **CustomSecurityTrimmerSample**, and then choose the **OK** button.</span></span>
    
  
4. <span data-ttu-id="c9496-128">В окне **Мастер настройки SharePoint** выберите **Развернуть как решение фермы** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c9496-128">In the **SharePoint Customization Wizard**, choose **Deploy as a farm solution**, and then choose **Finish**.</span></span>
    
  

### <a name="to-add-references-to-the-custom-security-trimmer-project"></a><span data-ttu-id="c9496-129">Добавление ссылок в проект настраиваемого триммера безопасности</span><span class="sxs-lookup"><span data-stu-id="c9496-129">To add references to the custom security trimmer project</span></span>


1. <span data-ttu-id="c9496-130">В меню **проект** выберите команду **Добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="c9496-130">On the **Project** menu, choose **Add Reference**.</span></span>
    
  
2. <span data-ttu-id="c9496-131">На вкладке **.NET** выберите ссылки со следующими именами компонентов и затем нажмите кнопку **ОК**:</span><span class="sxs-lookup"><span data-stu-id="c9496-131">On the **.NET** tab, choose the references with the following component names, and then choose the **OK** button:</span></span>
    
  - <span data-ttu-id="c9496-132">**Компонент Microsoft Search**</span><span class="sxs-lookup"><span data-stu-id="c9496-132">**Microsoft Search component**</span></span>
    
    <span data-ttu-id="c9496-p105">Вы должны увидеть две записи на вкладке **.NET** с именем компонент **компонент Microsoft Search**. Выберите запись, где столбца "путь"  это \\ISAPI\\Microsoft.Office.Server.Search.dll. При отсутствии на вкладке **.NET** в диалоговом окне **Добавление ссылок**, необходимо добавить ссылку на вкладке **Обзор**, используя путь к Microsoft.Office.Server.Search.dll.</span><span class="sxs-lookup"><span data-stu-id="c9496-p105">You should see two entries on the **.NET** tab with the component name **Microsoft Search component**. Select the entry where the Path column is \\ISAPI\\Microsoft.Office.Server.Search.dll. If this entry is missing from the **.NET** tab in the **Add References** dialog box, you must add the reference from the **Browse** tab by using the path to the Microsoft.Office.Server.Search.dll.</span></span>
    
  
  - <span data-ttu-id="c9496-136">**Microsoft.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="c9496-136">**Microsoft.IdentityModel**</span></span>
    
    <span data-ttu-id="c9496-137">Если на вкладке **.NET** **компонент Microsoft.IdentityModel** отсутствует, необходимо добавить ссылку на Microsoft.IdentityModel.dll на вкладке **Обзор** с помощью по следующему пути:</span><span class="sxs-lookup"><span data-stu-id="c9496-137">If **Microsoft.IdentityModel** is not listed on the **.NET** tab, you must add the reference to the Microsoft.IdentityModel.dll from the **Browse** tab, by using the following path:</span></span>
    
     `%ProgramFiles%\\Reference Assemblies\\Microsoft\\Windows Identity Foundation\\v4.0.`
    
  

## <a name="create-a-custom-security-pre-trimmer"></a><span data-ttu-id="c9496-138">Создание пользовательского предварительной триммера безопасности</span><span class="sxs-lookup"><span data-stu-id="c9496-138">Create a custom security pre-trimmer</span></span>
<span data-ttu-id="c9496-139"><a name="CreatePreTrimmer"> </a></span><span class="sxs-lookup"><span data-stu-id="c9496-139"><a name="CreatePreTrimmer"> </a></span></span>


### <a name="to-create-the-class-file-for-the-security-pre-trimmer"></a><span data-ttu-id="c9496-140">Чтобы создать файл класса для подготовки триммера безопасности</span><span class="sxs-lookup"><span data-stu-id="c9496-140">To create the class file for the security pre-trimmer</span></span>


1. <span data-ttu-id="c9496-141">В меню **ПРОЕКТ** выберите пункт **Добавить новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="c9496-141">On the **Project** menu, choose **Add New Item**.</span></span>
    
  
2. <span data-ttu-id="c9496-142">В разделе **Элементы Visual C#** в разделе **Установленные шаблоны** выберите **код** и нажмите кнопку **класса**.</span><span class="sxs-lookup"><span data-stu-id="c9496-142">Under **Visual C# Items** in **Installed Templates**, choose **Code**, and then choose **Class**.</span></span>
    
  
3. <span data-ttu-id="c9496-143">Введите **CustomSecurityPreTrimmer.cs** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c9496-143">Type **CustomSecurityPreTrimmer.cs**, and then choose **Add**.</span></span>
    
  

### <a name="writing-the-custom-security-pre-trimmer-code"></a><span data-ttu-id="c9496-144">Написание кода предварительной фильтрации по ролям безопасности</span><span class="sxs-lookup"><span data-stu-id="c9496-144">Writing the custom security pre-trimmer code</span></span>

<span data-ttu-id="c9496-p106">Ваше настраиваемого триммера безопасности необходимо реализовать интерфейс **ISecurityTrimmerPre**. В следующем примере кода  это базовая реализацию этого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c9496-p106">Your custom security trimmer must implement the **ISecurityTrimmerPre** interface. The following code example is a basic implementation of this interface.</span></span>
  
    
    

### <a name="to-modify-the-default-code-in-customsecuritypretrimmer"></a><span data-ttu-id="c9496-147">Изменение кода по умолчанию в CustomSecurityPreTrimmer</span><span class="sxs-lookup"><span data-stu-id="c9496-147">To modify the default code in CustomSecurityPreTrimmer</span></span>


1. <span data-ttu-id="c9496-148">Добавьте в начало класса следующие директивы **using**.</span><span class="sxs-lookup"><span data-stu-id="c9496-148">Add the following **using** directives at the beginning of the class.</span></span>
    
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

2. <span data-ttu-id="c9496-149">Укажите, что класс **CustomSecurityPreTrimmer** реализует интерфейс [ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) в объявлении класса, как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="c9496-149">Specify that the **CustomSecurityPreTrimmer** class implements the [ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) interface in the class declaration, as shown in the following code.</span></span>
    
```cs
  
public class CustomSecurityPreTrimmer : ISecurityTrimmerPre
```


### <a name="to-implement-the-isecuritytrimmerpre-interface-methods"></a><span data-ttu-id="c9496-150">Реализация методов интерфейса ISecurityTrimmerPre</span><span class="sxs-lookup"><span data-stu-id="c9496-150">To implement the ISecurityTrimmerPre interface methods</span></span>


1. <span data-ttu-id="c9496-151">Добавьте следующий код для объявления метода  [Initialize()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.Initialize.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c9496-151">Add the following code for the  [Initialize()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.Initialize.aspx) method declaration.</span></span>
    
```cs
  public void Initialize(NameValueCollection staticProperties, SearchServiceApplication searchApplication)
{

}
```


    The basic version of this sample does not include any code in the **Initialize** method.
    
  
2. <span data-ttu-id="c9496-152">Добавьте следующий код для объявления метода  [AddAccess()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.AddAccess.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c9496-152">Add the following code for the  [AddAccess()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.AddAccess.aspx) method declaration.</span></span>
    
```cs
  
public IEnumerable<Tuple<Claim, bool>> AddAccess(
                IDictionary<string, object> sessionProperties, IIdentity passedUserIdentity)
{
//AddAccess method implementation, see steps 3-5.
}
```

3. <span data-ttu-id="c9496-153">В первой части реализации метода **AddAccess** Узнайте пользователей, которые пользователь является, посмотрев _passedUserIdentity_.</span><span class="sxs-lookup"><span data-stu-id="c9496-153">For the first part of the **AddAccess** method implementation, we find out who the user is by looking at the _passedUserIdentity_.</span></span>
    
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

4. <span data-ttu-id="c9496-154">Создание списка, в списке с помощью утверждений и возврата списка, как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="c9496-154">Create a list, populate the list with claims and return the list, as shown in the following code.</span></span>
    
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
    
  

## <a name="create-a-custom-security-post-trimmer"></a><span data-ttu-id="c9496-155">Создание пользовательского после триммера безопасности</span><span class="sxs-lookup"><span data-stu-id="c9496-155">Create a custom security post-trimmer</span></span>
<span data-ttu-id="c9496-156"><a name="CreatePostTrimmer"> </a></span><span class="sxs-lookup"><span data-stu-id="c9496-156"></span></span>


### <a name="to-create-the-class-file-for-the-security-post-trimmer"></a><span data-ttu-id="c9496-157">Чтобы создать файл класса для триммера безопасности после завершения</span><span class="sxs-lookup"><span data-stu-id="c9496-157">To create the class file for the security post-trimmer</span></span>


1. <span data-ttu-id="c9496-158">В меню **ПРОЕКТ** выберите пункт **Добавить новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="c9496-158">On the **Project** menu, choose **Add New Item**.</span></span>
    
  
2. <span data-ttu-id="c9496-159">В разделе **Элементы Visual C#** в разделе **Установленные шаблоны** выберите **код**, а затем выберите **класс**...</span><span class="sxs-lookup"><span data-stu-id="c9496-159">Under **Visual C# Items** in **Installed Templates**, choose **Code**, and then choose **Class**..</span></span>
    
  
3. <span data-ttu-id="c9496-160">Введите CustomSecurityPostTrimmer.csи нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c9496-160">Type CustomSecurityPostTrimmer.cs, and then choose **Add**.</span></span>
    
  

### <a name="writing-the-custom-security-post-trimmer-code"></a><span data-ttu-id="c9496-161">Написание кода после фильтрации по ролям безопасности</span><span class="sxs-lookup"><span data-stu-id="c9496-161">Writing the custom security post-trimmer code</span></span>

<span data-ttu-id="c9496-p107">Ваше настраиваемого триммера безопасности необходимо реализовать интерфейс **ISecurityTrimmerPost**. В примере кода в этом разделе представлена базовая реализацию этого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c9496-p107">Your custom security trimmer must implement the **ISecurityTrimmerPost** interface. The code example in this section is a basic implementation of this interface.</span></span>
  
    
    

### <a name="to-modify-the-default-code-in-customsecurityposttrimmer"></a><span data-ttu-id="c9496-164">Изменение кода по умолчанию в CustomSecurityPostTrimmer</span><span class="sxs-lookup"><span data-stu-id="c9496-164">To modify the default code in CustomSecurityPostTrimmer</span></span>


1. <span data-ttu-id="c9496-165">Добавьте в начало класса следующие директивы **using**.</span><span class="sxs-lookup"><span data-stu-id="c9496-165">Add the following **using** directives at the beginning of the class:</span></span>
    
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

2. <span data-ttu-id="c9496-166">Укажите, что класс **CustomSecurityPostTrimmer** реализует интерфейс [ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) в объявлении класса следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c9496-166">Specify that the **CustomSecurityPostTrimmer** class implements the [ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) interface in the class declaration, as follows:</span></span>
    
```cs
  
public class CustomSecurityPostTrimmer : ISecurityTrimmerPost
```


### <a name="to-implement-the-isecuritytrimmerpost-interface-methods"></a><span data-ttu-id="c9496-167">Реализация методов интерфейса ISecurityTrimmerPost</span><span class="sxs-lookup"><span data-stu-id="c9496-167">To implement the ISecurityTrimmerPost interface methods</span></span>


1. <span data-ttu-id="c9496-168">Добавьте следующий код для объявления метода  [Initialize()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.Initialize.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c9496-168">Add the following code for the  [Initialize()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.Initialize.aspx) method declaration.</span></span>
    
```cs
  public void Initialize(NameValueCollection staticProperties, SearchServiceApplication searchApplication)
{

}
```


    The basic version of this sample does not include any code in the Initialize method.
    
  
2. <span data-ttu-id="c9496-169">Добавьте следующий код для объявления метода  [CheckAccess()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.CheckAccess.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c9496-169">Add the following code for the  [CheckAccess()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.CheckAccess.aspx) method declaration.</span></span>
    
```cs
  
public BitArray CheckAccess(IList<string> documentCrawlUrls, IList<string> documentAcls, IDictionary<string, object> sessionProperties, IIdentity passedUserIdentity)
{
//CheckAccess method implementation, see steps 3-5.
}
```

3. <span data-ttu-id="c9496-170">Первая часть реализации метода **CheckAccess** объявить и инициализировать переменную **BitArray** для хранения результатов проверки доступа для каждого URL-адреса в коллекции **documentCrawlUrls** и извлечения пользователя, который отправил запрос, как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="c9496-170">For the first part of the **CheckAccess** method implementation, declare and initialize a **BitArray** variable to store the results of the access check for each URL in the **documentCrawlUrls** collection, and retrieve the user who submitted the query, as shown in the following code.</span></span>
    
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

4. <span data-ttu-id="c9496-171">Пройдитесь по каждой URL-адрес обхода в коллекции и выполните проверку доступа, чтобы определить, если пользователь, отправивший запрос можно получить доступ к URL-адрес обхода связанного элемента контента, как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="c9496-171">Loop through each crawl URL in the collection, and perform the access check to determine if the user who submitted the query can access the crawl URL's associated content item, as shown in the following code.</span></span> 
    
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
    
  
5. <span data-ttu-id="c9496-172">Значение возвращаемое значение метода **CheckAccess** **urlStatusArray**, как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="c9496-172">Set the return value of the **CheckAccess** method to **urlStatusArray**, as shown in the following code.</span></span>
    
```cs
  
return urlStatusArray;
```


## <a name="register-the-custom-security-trimmer"></a><span data-ttu-id="c9496-173">Зарегистрируйте пользовательский триммер безопасности.</span><span class="sxs-lookup"><span data-stu-id="c9496-173">Register the custom security trimmer</span></span>
<span data-ttu-id="c9496-174"><a name="RegisterTrimmer"> </a></span><span class="sxs-lookup"><span data-stu-id="c9496-174"></span></span>

<span data-ttu-id="c9496-175">Этот шаг описывается настройка настраиваемого триммера безопасности и включает в себя следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="c9496-175">This step describes how to configure the custom security trimmer, and includes the following tasks:</span></span>
  
    
    

- <span data-ttu-id="c9496-176">Регистрация настраиваемого триммера безопасности для приложения службы поиска с помощью командлетов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c9496-176">Registering the custom security trimmer for the Search service application by using the Windows PowerShell cmdlets.</span></span>
    
  
- <span data-ttu-id="c9496-177">Перезапуск SharePoint хост-контроллер поиска (SPSearchHostController).</span><span class="sxs-lookup"><span data-stu-id="c9496-177">Restarting the SharePoint search host controller (SPSearchHostController).</span></span>
    
  

### <a name="register-the-custom-security-trimmer"></a><span data-ttu-id="c9496-178">Зарегистрируйте пользовательский триммер безопасности.</span><span class="sxs-lookup"><span data-stu-id="c9496-178">Register the custom security trimmer</span></span>

<span data-ttu-id="c9496-p108">Используйте Командная консоль SharePoint для регистрации настраиваемого триммера безопасности в  _ClassName_. В нашем случае  _ClassName_ может быть **CustomSecurityPreTrimmer** или **CustomSecurityPostTrimmer**. В следующей процедуре показано, как зарегистрировать пользовательский триммер безопасности, с Идентификатором, равным 1 для приложения службы поиска.</span><span class="sxs-lookup"><span data-stu-id="c9496-p108">You use the SharePoint Management Shell to register a custom security trimmer with  _ClassName_. In our case,  _ClassName_ could be either **CustomSecurityPreTrimmer** or **CustomSecurityPostTrimmer**. The following procedure shows how to register a custom security trimmer, with the ID set to 1 for the Search service application.</span></span>
  
    
    

### <a name="to-register-the-custom-security-trimmer"></a><span data-ttu-id="c9496-182">Регистрация настраиваемого триммера безопасности</span><span class="sxs-lookup"><span data-stu-id="c9496-182">To register the custom security trimmer</span></span>


1. <span data-ttu-id="c9496-183">В проводнике найдите файл CustomSecurityTrimmerSample.dll, расположенный в каталоге  _<Local_Drive>_:\\WINDOWS\\assembly.</span><span class="sxs-lookup"><span data-stu-id="c9496-183">In Windows Explorer, locate CustomSecurityTrimmerSample.dll in the path  _<Local_Drive>_:\\WINDOWS\\assembly.</span></span>
    
  
2. <span data-ttu-id="c9496-184">Откройте контекстное меню для файла и выберите пункт Свойства.</span><span class="sxs-lookup"><span data-stu-id="c9496-184">Open the shortcut menu for the file, and then choose Properties.</span></span>
    
  
3. <span data-ttu-id="c9496-185">На вкладке **Общие** диалогового окна **Свойства** выберите и скопируйте маркер.</span><span class="sxs-lookup"><span data-stu-id="c9496-185">On the **General** tab in the **Properties** dialog box, select the token and copy it.</span></span>
    
  
4. <span data-ttu-id="c9496-p109">Откройте Командная консоль SharePoint. Сведения об использовании этого средства можно  [Администрирование приложений-служб с помощью консоли управления SharePoint 2010](http://msdn.microsoft.com/library/aff64855-7377-4e4a-b3a9-b620c9047076%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="c9496-p109">Open the SharePoint Management Shell. For information about using this tool, see  [Administering Service Applications Using the SharePoint 2010 Management Shell](http://msdn.microsoft.com/library/aff64855-7377-4e4a-b3a9-b620c9047076%28Office.15%29.aspx)</span></span>
    
  
5. <span data-ttu-id="c9496-188">Введите в командной строке следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c9496-188">At the command prompt, type the following command.</span></span>
    
```
  New-SPEnterpriseSearchSecurityTrimmer -SearchApplication "Search Service Application"
-typeName "CustomSecurityTrimmerSample.ClassName, CustomSecurityTrimmerSample, 
Version=1.0.0.0, Culture=neutral, PublicKeyToken=token" -RulePath "xmldoc://*"
```


    In the command, replace  _ClassName_ either with **CustomSecurityPreTrimmer** or **CustomSecurityPostTrimmer** and _token_ with the Public Key Token for the CustomSecurityTrimmerSample.dll file. You must associate all post-trimmers with a crawl rule, _"xmldoc://*"_; but this is optional for pre-trimmers.
    
    > [!NOTE]
    > If you have multiple front-end web servers, you must deploy your security trimmer to the global assembly cache on all the front-end web servers in the farm. 

6. <span data-ttu-id="c9496-189">Убедитесь, что следующие командлеты PowerShell зарегистрирован триммер безопасности.</span><span class="sxs-lookup"><span data-stu-id="c9496-189">Verify that your security trimmer is registered with the following PowerShell cmdlets.</span></span>
    
```
  
$searchApp = Get-SPEnterpriseSearchServiceApplication
$searchApp | Get-SPEnterpriseSearchSecurityTrimmer
```


    Your security trimmer must be visible in the results.
    
  

### <a name="to-restart-the-sharepoint-search-host-controller"></a><span data-ttu-id="c9496-190">Чтобы перезапустить хост-контроллер поиска SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9496-190">To restart the SharePoint search host controller</span></span>


- <span data-ttu-id="c9496-191">Можно перезапустить службу поиска, введя следующий командлет PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c9496-191">You can restart the Search Service by typing the following PowerShell cmdlet.</span></span>
    
```
  
net restart sphostcontrollerservice

```


## <a name="see-also"></a><span data-ttu-id="c9496-192">См. также</span><span class="sxs-lookup"><span data-stu-id="c9496-192">See also</span></span>
<span data-ttu-id="c9496-193"><a name="bk_sectrimmer_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c9496-193"></span></span>


-  [<span data-ttu-id="c9496-194">Специальная фильтрация по ролям безопасности, настраиваемая для поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9496-194">Custom security trimming for Search in SharePoint</span></span>](custom-security-trimming-for-search-in-sharepoint-server.md)
    
  
-  [<span data-ttu-id="c9496-195">Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre</span><span class="sxs-lookup"><span data-stu-id="c9496-195">Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx)
    
  
-  [<span data-ttu-id="c9496-196">Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost</span><span class="sxs-lookup"><span data-stu-id="c9496-196">Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx)
    
  
-  [<span data-ttu-id="c9496-197">Microsoft.Office.Server.Search.Query.PluggableAccessCheckException</span><span class="sxs-lookup"><span data-stu-id="c9496-197">Microsoft.Office.Server.Search.Query.PluggableAccessCheckException</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.PluggableAccessCheckException.aspx)
    
  

