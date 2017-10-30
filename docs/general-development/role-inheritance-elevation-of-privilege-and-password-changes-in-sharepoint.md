---
title: "Роли, наследования, несанкционированное получение прав и изменения паролей в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 6860c6c126d3d617e303ec4bd67f73236eb647d0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="role-inheritance-elevation-of-privilege-and-password-changes-in-sharepoint"></a><span data-ttu-id="22510-102">Роли, наследования, несанкционированное получение прав и изменения паролей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="22510-102">Role, inheritance, elevation of privilege, and password changes in SharePoint</span></span>

## <a name="roles-role-definitions-and-role-assignments"></a><span data-ttu-id="22510-103">Роли, определения ролей и назначения ролей</span><span class="sxs-lookup"><span data-stu-id="22510-103">Roles, role definitions, and role assignments</span></span>
<span data-ttu-id="22510-104"><a name="SP15_RoleInheritance_Role"> </a></span><span class="sxs-lookup"><span data-stu-id="22510-104"></span></span>

<span data-ttu-id="22510-105">Роль состоит из двух частей: из определения и назначения.</span><span class="sxs-lookup"><span data-stu-id="22510-105">A role consists of two parts: a role definition and a role assignment.</span></span> 
  
    
    
<span data-ttu-id="22510-p101">Определение роли или уровень разрешений,  это список прав, связанных с ролью. Право является уникальным образом управляемое действие в рамках веб-сайта SharePoint. Например, для пользователей с ролью **Read** можно просматривать страницы веб-сайта и просмотр элементов в списках. Разрешения пользователей никогда не осуществляется непосредственно с помощью прав. Все разрешения пользователей и групп можно управлять с помощью ролей. Определение роли  это набор прав, привязанные к конкретному объекту. Определения ролей (например, **Full Control**, **Read**, **Contribute**, **Design**или **Limited Access**), находятся на веб-сайт и имеют одинаковые значения везде в пределах веб-сайта, но их значения может быть различным всех сайтов в пределах одного семейства сайтов. Определения ролей можно также наследуется от родительского веб-сайта, так же, как можно унаследованные разрешения.</span><span class="sxs-lookup"><span data-stu-id="22510-p101">The role definition, or permission level, is the list of rights associated with the role. A right is a uniquely controllable action within a SharePoint website. For example, a user with the **Read** role can browse pages in the website and view items in lists. User permissions are never managed directly by using rights. All user and group permissions are managed through roles. A role definition is a collection of rights bound to a specific object. Role definitions (for example, **Full Control**, **Read**, **Contribute**, **Design**, or **Limited Access**) are scoped to the website and mean the same thing everywhere within the website, but their meanings can differ between sites within the same site collection. Role definitions can also be inherited from the parent website, just as permissions can be inherited.</span></span> 
  
    
    
<span data-ttu-id="22510-114">Назначение ролей — это отношение между определения роли, пользователи и группы и области действия (например, один пользователь может быть чтения в списке 1, во время чтения в списке 2 другому пользователю).</span><span class="sxs-lookup"><span data-stu-id="22510-114">The role assignment is the relationship among the role definition, the users and groups, and the scope (for example, one user may be a reader on list 1, while another user is a reader on list 2).</span></span> <span data-ttu-id="22510-115">Отношение выразить через назначение ролей — ключ для реализации управления безопасности SharePoint на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="22510-115">The relationship expressed through the role assignment is the key to making SharePoint security management role-based.</span></span> <span data-ttu-id="22510-116">Все разрешения можно управлять с помощью роли. никогда не следует назначить права непосредственно пользователю.</span><span class="sxs-lookup"><span data-stu-id="22510-116">All permissions are managed through roles; you never assign rights directly to a user.</span></span> <span data-ttu-id="22510-117">Назначьте только удобной для восприятия коллекций прав (определения ролей), которые являются хорошо определенные и согласованность.</span><span class="sxs-lookup"><span data-stu-id="22510-117">You assign only meaningful collections of rights (role definitions) that are well-defined and consistent.</span></span> <span data-ttu-id="22510-118">Путем добавления или удаления пользователей и групп для или из определения ролей через назначения ролей для управления уникальные разрешения.</span><span class="sxs-lookup"><span data-stu-id="22510-118">You manage unique permissions by adding or removing users and groups to or from role definitions through role assignments.</span></span>
  
    
    
<span data-ttu-id="22510-119">Администратор веб-сайта можно настроить определения ролей и создать дополнительные настраиваемые роли с помощью страницы управления ролями, в котором перечислены определения ролей, доступные на сайте.</span><span class="sxs-lookup"><span data-stu-id="22510-119">The website administrator can customize the default role definitions and create additional custom roles by using the Manage Roles page, which lists the available role definitions in the site.</span></span>
  
    
    

## <a name="role-definition-inheritance"></a><span data-ttu-id="22510-120">Наследование определений ролей</span><span class="sxs-lookup"><span data-stu-id="22510-120">Role definition inheritance</span></span>
<span data-ttu-id="22510-121"><a name="SP15_RoleInheritance_RoleDefInheritance"> </a></span><span class="sxs-lookup"><span data-stu-id="22510-121"></span></span>

<span data-ttu-id="22510-122">Нарушение наследования определения роли необходимо также нарушение наследования разрешений SharePoint поддерживает наследующие определения ролей аналогично тому, как он поддерживает наследование разрешений</span><span class="sxs-lookup"><span data-stu-id="22510-122">SharePoint supports inheriting role definitions similarly to how it supports inheriting permissions, and breaking role definition inheritance requires also breaking permissions inheritance.</span></span>
  
    
    
<span data-ttu-id="22510-123">Каждый объект SharePoint может иметь собственный набор разрешений или наследовать разрешения от родительского контейнера.</span><span class="sxs-lookup"><span data-stu-id="22510-123">Each SharePoint object can have its own set of permissions or inherit its permissions from its parent container.</span></span> <span data-ttu-id="22510-124">SharePoint не поддерживает частичный наследования, где будет наследовать все разрешения родительского и есть некоторые собственные разрешения объекта.</span><span class="sxs-lookup"><span data-stu-id="22510-124">SharePoint does not support partial inheritance, where an object would inherit all the permissions of its parent and also have some of its own permissions.</span></span> <span data-ttu-id="22510-125">Уникальные или наследуемые разрешения:</span><span class="sxs-lookup"><span data-stu-id="22510-125">Permissions are either unique or inherited.</span></span> <span data-ttu-id="22510-126">SharePoint не поддерживает расширенный наследования.</span><span class="sxs-lookup"><span data-stu-id="22510-126">SharePoint does not support directed inheritance.</span></span> <span data-ttu-id="22510-127">Например объект могут наследовать только от его родительского контейнера, не из других объектов или контейнера.</span><span class="sxs-lookup"><span data-stu-id="22510-127">For example, an object can inherit only from its parent container, not from some other object or container.</span></span>
  
    
    
<span data-ttu-id="22510-p104">Когда веб-сайт наследует определения ролей, ролей доступны только для чтения, как разрешения только для чтения в наследуемые веб-сайта. Пользователь может перейти к родительского сайта, в котором содержатся уникальные определения ролей через ссылку. Значение по умолчанию для всех новых веб-сайтов, даже сайты с уникальными разрешениями  наследование определений ролей из родительского веб-сайта. Когда уникальные разрешения, определения ролей можно вернуть для определения унаследованного ролей или изменены как определения локальной роли.</span><span class="sxs-lookup"><span data-stu-id="22510-p104">When a website inherits role definitions, the roles are read-only, like the read-only permissions in an inherited website. The user can navigate to the parent site that holds the unique role definitions via a link. The default setting for all new websites, even sites with unique permissions, is to inherit role definitions from the parent website. When the permissions are unique, role definitions can be reverted to inherited role definitions or edited as local role definitions.</span></span>
  
    
    
<span data-ttu-id="22510-132">Наследование определений ролей на веб-сайте влияет на наследование разрешений следующих правил:</span><span class="sxs-lookup"><span data-stu-id="22510-132">Role definition inheritance in a website affects permissions inheritance following these rules:</span></span>
  
    
    

- <span data-ttu-id="22510-133">Разрешения наследуются только в том случае, если также происходит наследование определений ролей.</span><span class="sxs-lookup"><span data-stu-id="22510-133">Cannot inherit permissions unless it also inherits role definitions.</span></span>
    
  
- <span data-ttu-id="22510-134">Уникальные определения ролей создаются только в том случае, если одновременно создаются уникальные разрешения.</span><span class="sxs-lookup"><span data-stu-id="22510-134">Cannot create unique role definitions unless it also creates unique permissions.</span></span>
    
  
- <span data-ttu-id="22510-p105">Замена на наследованные определения ролей происходит только в том случае, если одновременно также заменяются все уникальные разрешения на веб-странице. Существующие разрешения зависят от определений ролей.</span><span class="sxs-lookup"><span data-stu-id="22510-p105">Cannot revert to inherited role definitions unless it also reverts all unique permissions within the website. The existing permissions are dependent on the role definitions.</span></span>
    
  
- <span data-ttu-id="22510-p106">Замена на наследуемые разрешения производится только в том случае, если одновременно происходит замена на наследуемые определения ролей. Разрешения веб-сайта всегда связаны с определениями ролей для этого веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="22510-p106">Cannot revert to inherited permissions unless it also reverts to inherited role definitions. The permissions for a website are always tied to the role definitions for that website.</span></span>
    
  

## <a name="managing-user-tokens"></a><span data-ttu-id="22510-139">Управление токенами пользователей</span><span class="sxs-lookup"><span data-stu-id="22510-139">Managing user tokens</span></span>
<span data-ttu-id="22510-140"><a name="SP15_RoleInheritance_ManagingUserTokens"> </a></span><span class="sxs-lookup"><span data-stu-id="22510-140"></span></span>

<span data-ttu-id="22510-p107">SharePoint извлекает сведения маркера пользователя из базы данных SharePoint. Если не выбрана сайта или маркер пользователя, созданный ранее более 24 часов, SharePoint создает новый маркер пользователя, пытается обновить список групп, к которым принадлежит пользователь.</span><span class="sxs-lookup"><span data-stu-id="22510-p107">SharePoint fetches user token information from the SharePoint database. If the user has never visited the site or if the user's token was generated more than 24 hours previously, SharePoint generates a new user token by trying to refresh the list of groups that the user belongs to.</span></span> 
  
    
    
<span data-ttu-id="22510-p108">Если учетная запись является учетной записью NT, SharePoint использует интерфейс **AuthZ** для запроса службы каталогов Active Directory для свойства **TokenGroups**. Это может отсутствовать, если SharePoint запущены в экстрасети режиме и не имеет разрешения на запрос Active Directory для данного свойства.</span><span class="sxs-lookup"><span data-stu-id="22510-p108">If the user account is an NT account, SharePoint uses the **AuthZ** interface to query the Active Directory directory service for the **TokenGroups** property. This may fail if SharePoint is running in an extranet mode, and does not have permission to query Active Directory for this property.</span></span>
  
    
    
<span data-ttu-id="22510-p109">Если учетная запись пользователя членства, SharePoint отправляет запрос ASP.NET **RoleManager** для всех ролей, к которым принадлежит пользователь. Это может завершиться ошибкой, если не соответствующие config-файла для текущего исполняемого файла.</span><span class="sxs-lookup"><span data-stu-id="22510-p109">If the user account is a membership user, SharePoint queries the ASP.NET **RoleManager** for all the roles that the user belongs to. This may fail if there is not a proper .config file for the current executable file.</span></span>
  
    
    
<span data-ttu-id="22510-p110">Если SharePoint не удается получить из Active Directory или **<roleManager>**пользователя в группах, недавно созданный маркер содержит только пользователя уникальный идентификатор безопасности (SID). Исключение не создается, но записи в журнал ULS сервера. Новый маркер также записывается в базу данных SharePoint, чтобы не повторно создается в течение 24 часов.</span><span class="sxs-lookup"><span data-stu-id="22510-p110">If SharePoint can't obtain the user's group memberships from Active Directory or **<roleManager>**, the newly generated token contains only the user's unique security ID (SID). No exception is thrown, but an entry is written into the ULS server log. The new token is also written into the SharePoint database so that it will not be regenerated within 24 hours.</span></span>
  
    
    
<span data-ttu-id="22510-p111">После SharePoint получает маркер новым из базы данных SharePoint или, создав новый маркер, SharePoint задает метки времени для текущего времени и возвращается пользователю для вызывающего абонента. Это гарантирует, что маркер является новым 24 часа.</span><span class="sxs-lookup"><span data-stu-id="22510-p111">After SharePoint obtains a fresh token, from the SharePoint database or by generating a new token, SharePoint sets the timestamp to be the current time and then returns it to the caller. This guarantees that the token is fresh for 24 hours.</span></span>
  
    
    
<span data-ttu-id="22510-p112">После объекта  [SPUserToken](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPUserToken.aspx) возвращается вызывающего абонента, отвечает вызывающего абонента не использовать маркер после срок его действия. Можно написать программу модуля поддержки для отслеживания срока действия токена, записав времени, когда получения маркера и сравнение копирования с текущего времени в [SPWebService.TokenTimeout](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPWebService.TokenTimeout.aspx) .</span><span class="sxs-lookup"><span data-stu-id="22510-p112">After the  [SPUserToken](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPUserToken.aspx) object is returned to the caller, it is the caller's responsibility to not use the token after it is expired. You can write a helper utility to track the token expiration by recording the time when you get the token, and compare the diff with current time against [SPWebService.TokenTimeout](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPWebService.TokenTimeout.aspx) .</span></span>
  
    
    
<span data-ttu-id="22510-p113">Если истекшие маркер используется для создания веб-сайта SharePoint,  это исключение. Значение маркера времени ожидания по умолчанию: 24 часа. Он может осуществляться с помощью  [SPWebService.TokenTimeout](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPWebService.TokenTimeout.aspx) .</span><span class="sxs-lookup"><span data-stu-id="22510-p113">If an expired token is used to create a SharePoint website, an exception is thrown. The default token timeout value is 24 hours. It can be accessed via  [SPWebService.TokenTimeout](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPWebService.TokenTimeout.aspx) .</span></span>
  
    
    

## <a name="elevation-of-privilege"></a><span data-ttu-id="22510-157">несанкционированное получение прав;</span><span class="sxs-lookup"><span data-stu-id="22510-157">Elevation of privilege</span></span>
<span data-ttu-id="22510-158"><a name="SP15_RoleInheritance_ElevationOfPrivilege"> </a></span><span class="sxs-lookup"><span data-stu-id="22510-158"></span></span>

<span data-ttu-id="22510-p114">Несанкционированное получение прав, компонент, который был добавлен в Службы Windows SharePoint Services 3.0 позволяет вам для программного выполнения действий в коде с помощью повышенного уровня прав. Метод  [SPSecurity.RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) позволяет предоставить делегата, на котором выполняется подмножество кода в контексте учетной записи с привилегиями выше, чем текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="22510-p114">Elevation of privilege, a feature that was added in Windows SharePoint Services 3.0, enables you to programmatically perform actions in code by using an increased level of privilege. The  [SPSecurity.RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) method enables you to supply a delegate that runs a subset of code in the context of an account with higher privileges than the current user.</span></span>
  
    
    
<span data-ttu-id="22510-161">Ниже приведен стандартного использования **RunWithElevatedPrivileges**.</span><span class="sxs-lookup"><span data-stu-id="22510-161">The following is a standard use of **RunWithElevatedPrivileges**.</span></span>
  
    
    



```cs

SPSecurity.RunWithElevatedPrivileges(delegate()
{
    // Do things by assuming the permission of the "system account".
});
```

<span data-ttu-id="22510-p115">Как правило для выполнения действий в SharePoint, необходимо получить новый объект  [SPSite](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSite.aspx) , чтобы увидеть результат изменений. Например:</span><span class="sxs-lookup"><span data-stu-id="22510-p115">Frequently, to perform actions in SharePoint, you must get a new  [SPSite](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSite.aspx) object to effect the changes. For example:</span></span>
  
    
    



```cs

SPSecurity.RunWithElevatedPrivileges(delegate()
{
    using (SPSite site = new SPSite(web.Site.ID))
    {
       // Do things by assuming the permission of the "system account".
    }
});
```

<span data-ttu-id="22510-p116">Несмотря на то, что несанкционированное получение прав предоставляет мощные метод для управления безопасностью, его следует использовать с осторожностью. Не следует предоставлять прямой, неконтролируемые механизмы для людей с низкими привилегиями для обхода разрешения, предоставленные им.</span><span class="sxs-lookup"><span data-stu-id="22510-p116">Although elevation of privilege provides a powerful technique for managing security, it should be used with care. You should not expose direct, uncontrolled mechanisms for people with low privileges to circumvent the permissions granted to them.</span></span>
  
    
    

> <span data-ttu-id="22510-166">**Важные:** Если метод, переданной в [RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) включает в себя все операции записи, вызов [RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) должен предшествовать вызов [SPUtility.ValidateFormDigest()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPUtility.ValidateFormDigest.aspx) или [SPWeb.ValidateFormDigest() ](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.ValidateFormDigest.aspx) .</span><span class="sxs-lookup"><span data-stu-id="22510-166">**Important:** If the method passed to  [RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) includes any write operations, the call to [RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) should be preceded by a call to either [SPUtility.ValidateFormDigest()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPUtility.ValidateFormDigest.aspx) or [SPWeb.ValidateFormDigest()](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.ValidateFormDigest.aspx) .</span></span>
  
    
    


## <a name="automatic-password-changes"></a><span data-ttu-id="22510-167">Автоматической смены пароля</span><span class="sxs-lookup"><span data-stu-id="22510-167">Automatic password changes</span></span>
<span data-ttu-id="22510-168"><a name="SP15_RoleInheritance_AutomaticPasswordChange"> </a></span><span class="sxs-lookup"><span data-stu-id="22510-168"></span></span>

<span data-ttu-id="22510-169">Функции изменения автоматической смены пароля позволяет обновлять и развертывание пароли без выполнения пароля вручную обновление задач в нескольких учетных записей, служб и веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="22510-169">The automatic password change feature enables you to update and deploy passwords without performing manual password update tasks across multiple accounts, services, and web applications.</span></span> <span data-ttu-id="22510-170">Это упрощает управление паролем в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="22510-170">This makes managing password in SharePoint simpler.</span></span> <span data-ttu-id="22510-171">Чтобы определить, является ли пароль истекает срок действия и сброс пароля с помощью строки в случайном порядке длинные, криптографически строгого можно использовать функции изменения автоматической смены пароля.</span><span class="sxs-lookup"><span data-stu-id="22510-171">You can use the automatic password change feature to determine whether a password is about to expire and to reset the password by using a long, cryptographically strong random string.</span></span>
  
    
    

### <a name="managed-account"></a><span data-ttu-id="22510-172">Управляемая учетная запись</span><span class="sxs-lookup"><span data-stu-id="22510-172">Managed account</span></span>

<span data-ttu-id="22510-p118">Использование управляемых учетных записей для реализации функции изменения автоматической смены пароля. Управляемые учетные записи повысить уровень безопасности и обеспечения изоляции приложений. Управляемые учетные записи можно выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="22510-p118">You use managed accounts to implement the automatic password change feature. Managed accounts improve security and ensure application isolation. With managed accounts, you can:</span></span>
  
    
    

- <span data-ttu-id="22510-176">Настройка функции изменения автоматической смены пароля для развертывания пароли для всех служб в ферме.</span><span class="sxs-lookup"><span data-stu-id="22510-176">Configure the automatic password change feature to deploy passwords across all services in a farm.</span></span>
    
  
- <span data-ttu-id="22510-177">Настройка веб-приложения SharePoint и службы, которые выполняются на серверах приложений в ферме SharePoint, для использования разными учетными записями домена.</span><span class="sxs-lookup"><span data-stu-id="22510-177">Configure SharePoint web applications and services, that are running on application servers in a SharePoint farm, to use different domain accounts.</span></span>
    
  
- <span data-ttu-id="22510-178">Сопоставление управляемых учетных записей для различных служб и веб-приложений в ферме.</span><span class="sxs-lookup"><span data-stu-id="22510-178">Map managed accounts to various services and web applications in a farm.</span></span>
    
  
- <span data-ttu-id="22510-179">Создание нескольких учетных записей в доменных службах Active Directory (AD DS) и регистрация каждого из этих учетных записей в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="22510-179">Create multiple accounts in Active Directory Domain Services (AD DS), and then register each of these accounts in SharePoint.</span></span>
    
  
<span data-ttu-id="22510-180">Можно также регистрация управляемых учетных записей и включить SharePoint для управления паролей учетных записей.</span><span class="sxs-lookup"><span data-stu-id="22510-180">You can also register managed accounts and enable SharePoint to control account passwords.</span></span> <span data-ttu-id="22510-181">Пользователи должны получать уведомления о изменения запланированных пароль и другие связанные службы, но учетные записи, используемые фермой SharePoint, веб-приложений и автоматически сбросить и развернуты в пределах фермы при необходимости, различных служб на основе настраивать расписания сброса пароля по отдельности.</span><span class="sxs-lookup"><span data-stu-id="22510-181">Users have to be notified about planned password changes and related service interruptions, but the accounts used by a SharePoint farm, web applications, and various services can be automatically reset and deployed within the farm as necessary, based on individually configured password reset schedules.</span></span>
  
    
    
<span data-ttu-id="22510-182">Операции, которые можно использовать класс  [SPManagedAccount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.aspx) для выполнения относятся:</span><span class="sxs-lookup"><span data-stu-id="22510-182">Operations that you can use the  [SPManagedAccount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.aspx) class to perform include:</span></span>
  
    
    

- <span data-ttu-id="22510-183">Изменение пароля</span><span class="sxs-lookup"><span data-stu-id="22510-183">Change password</span></span>
    
  
- <span data-ttu-id="22510-184">Задать расписание смены паролей</span><span class="sxs-lookup"><span data-stu-id="22510-184">Set a password change schedule</span></span>
    
  
- <span data-ttu-id="22510-185">Распространения смены пароля</span><span class="sxs-lookup"><span data-stu-id="22510-185">Propagate password change</span></span>
    
  
- <span data-ttu-id="22510-186">Определить, когда последнего изменения пароля</span><span class="sxs-lookup"><span data-stu-id="22510-186">Find out when a password was last changed</span></span>
    
  
- <span data-ttu-id="22510-187">Принудительное применение Минимальная длина пароля</span><span class="sxs-lookup"><span data-stu-id="22510-187">Enforce minimum length for password</span></span>
    
  
<span data-ttu-id="22510-188">Дополнительные сведения об API управляемой учетной записи можно найти по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="22510-188">For more information about the managed account API, see the following links:</span></span>
  
    
    

-  [<span data-ttu-id="22510-189">SPManagedAccount</span><span class="sxs-lookup"><span data-stu-id="22510-189">SPManagedAccount</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.aspx)
    
  
-  [<span data-ttu-id="22510-190">SPManagedAccount.EventProcessingOptions</span><span class="sxs-lookup"><span data-stu-id="22510-190">SPManagedAccount.EventProcessingOptions</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.EventProcessingOptions.aspx)
    
  
-  [<span data-ttu-id="22510-191">SPManagedAccount.EventType</span><span class="sxs-lookup"><span data-stu-id="22510-191">SPManagedAccount.EventType</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.EventType.aspx)
    
  

## <a name="additional-resources"></a><span data-ttu-id="22510-192">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="22510-192">Additional resources</span></span>
<span data-ttu-id="22510-193"><a name="SP15_RoleInheritance_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="22510-193"></span></span>


-  [<span data-ttu-id="22510-194">Проверка подлинности, авторизация и безопасность в SharePoint</span><span class="sxs-lookup"><span data-stu-id="22510-194">Authentication, authorization, and security in SharePoint</span></span>](authentication-authorization-and-security-in-sharepoint.md)
    
  
-  [<span data-ttu-id="22510-195">Авторизация, пользователи, группы и объектная модель в SharePoint</span><span class="sxs-lookup"><span data-stu-id="22510-195">Authorization, users, groups, and the object model in SharePoint</span></span>](authorization-users-groups-and-the-object-model-in-sharepoint.md)
    
  
-  [<span data-ttu-id="22510-196">Удостоверение, основанное на основе утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="22510-196">Claims-based identity in SharePoint</span></span>](claims-based-identity-in-sharepoint.md)
    
  
-  [<span data-ttu-id="22510-197">Удостоверение, основанное на утверждениях и концепций в SharePoint</span><span class="sxs-lookup"><span data-stu-id="22510-197">Claims-based identity and concepts in SharePoint</span></span>](claims-based-identity-and-concepts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="22510-198">Настройки, администрирования и ресурсы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="22510-198">Configuration, administration, and resources in SharePoint</span></span>](configuration-administration-and-resources-in-sharepoint.md)
    
  

