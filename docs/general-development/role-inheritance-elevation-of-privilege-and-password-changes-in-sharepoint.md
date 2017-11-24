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
# <a name="role-inheritance-elevation-of-privilege-and-password-changes-in-sharepoint"></a>Роли, наследования, несанкционированное получение прав и изменения паролей в SharePoint

## <a name="roles-role-definitions-and-role-assignments"></a>Роли, определения ролей и назначения ролей
<a name="SP15_RoleInheritance_Role"> </a>

Роль состоит из двух частей: из определения и назначения. 
  
    
    
Определение роли или уровень разрешений,  это список прав, связанных с ролью. Право является уникальным образом управляемое действие в рамках веб-сайта SharePoint. Например, для пользователей с ролью **Read** можно просматривать страницы веб-сайта и просмотр элементов в списках. Разрешения пользователей никогда не осуществляется непосредственно с помощью прав. Все разрешения пользователей и групп можно управлять с помощью ролей. Определение роли  это набор прав, привязанные к конкретному объекту. Определения ролей (например, **Full Control**, **Read**, **Contribute**, **Design**или **Limited Access**), находятся на веб-сайт и имеют одинаковые значения везде в пределах веб-сайта, но их значения может быть различным всех сайтов в пределах одного семейства сайтов. Определения ролей можно также наследуется от родительского веб-сайта, так же, как можно унаследованные разрешения. 
  
    
    
Назначение ролей — это отношение между определения роли, пользователи и группы и области действия (например, один пользователь может быть чтения в списке 1, во время чтения в списке 2 другому пользователю). Отношение выразить через назначение ролей — ключ для реализации управления безопасности SharePoint на основе ролей. Все разрешения можно управлять с помощью роли. никогда не следует назначить права непосредственно пользователю. Назначьте только удобной для восприятия коллекций прав (определения ролей), которые являются хорошо определенные и согласованность. Путем добавления или удаления пользователей и групп для или из определения ролей через назначения ролей для управления уникальные разрешения.
  
    
    
Администратор веб-сайта можно настроить определения ролей и создать дополнительные настраиваемые роли с помощью страницы управления ролями, в котором перечислены определения ролей, доступные на сайте.
  
    
    

## <a name="role-definition-inheritance"></a>Наследование определений ролей
<a name="SP15_RoleInheritance_RoleDefInheritance"> </a>

Нарушение наследования определения роли необходимо также нарушение наследования разрешений SharePoint поддерживает наследующие определения ролей аналогично тому, как он поддерживает наследование разрешений
  
    
    
Каждый объект SharePoint может иметь собственный набор разрешений или наследовать разрешения от родительского контейнера. SharePoint не поддерживает частичный наследования, где будет наследовать все разрешения родительского и есть некоторые собственные разрешения объекта. Уникальные или наследуемые разрешения: SharePoint не поддерживает расширенный наследования. Например объект могут наследовать только от его родительского контейнера, не из других объектов или контейнера.
  
    
    
Когда веб-сайт наследует определения ролей, ролей доступны только для чтения, как разрешения только для чтения в наследуемые веб-сайта. Пользователь может перейти к родительского сайта, в котором содержатся уникальные определения ролей через ссылку. Значение по умолчанию для всех новых веб-сайтов, даже сайты с уникальными разрешениями  наследование определений ролей из родительского веб-сайта. Когда уникальные разрешения, определения ролей можно вернуть для определения унаследованного ролей или изменены как определения локальной роли.
  
    
    
Наследование определений ролей на веб-сайте влияет на наследование разрешений следующих правил:
  
    
    

- Разрешения наследуются только в том случае, если также происходит наследование определений ролей.
    
  
- Уникальные определения ролей создаются только в том случае, если одновременно создаются уникальные разрешения.
    
  
- Замена на наследованные определения ролей происходит только в том случае, если одновременно также заменяются все уникальные разрешения на веб-странице. Существующие разрешения зависят от определений ролей.
    
  
- Замена на наследуемые разрешения производится только в том случае, если одновременно происходит замена на наследуемые определения ролей. Разрешения веб-сайта всегда связаны с определениями ролей для этого веб-сайта.
    
  

## <a name="managing-user-tokens"></a>Управление токенами пользователей
<a name="SP15_RoleInheritance_ManagingUserTokens"> </a>

SharePoint извлекает сведения маркера пользователя из базы данных SharePoint. Если не выбрана сайта или маркер пользователя, созданный ранее более 24 часов, SharePoint создает новый маркер пользователя, пытается обновить список групп, к которым принадлежит пользователь. 
  
    
    
Если учетная запись является учетной записью NT, SharePoint использует интерфейс **AuthZ** для запроса службы каталогов Active Directory для свойства **TokenGroups**. Это может отсутствовать, если SharePoint запущены в экстрасети режиме и не имеет разрешения на запрос Active Directory для данного свойства.
  
    
    
Если учетная запись пользователя членства, SharePoint отправляет запрос ASP.NET **RoleManager** для всех ролей, к которым принадлежит пользователь. Это может завершиться ошибкой, если не соответствующие config-файла для текущего исполняемого файла.
  
    
    
Если SharePoint не удается получить из Active Directory или **<roleManager>**пользователя в группах, недавно созданный маркер содержит только пользователя уникальный идентификатор безопасности (SID). Исключение не создается, но записи в журнал ULS сервера. Новый маркер также записывается в базу данных SharePoint, чтобы не повторно создается в течение 24 часов.
  
    
    
После SharePoint получает маркер новым из базы данных SharePoint или, создав новый маркер, SharePoint задает метки времени для текущего времени и возвращается пользователю для вызывающего абонента. Это гарантирует, что маркер является новым 24 часа.
  
    
    
После объекта  [SPUserToken](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPUserToken.aspx) возвращается вызывающего абонента, отвечает вызывающего абонента не использовать маркер после срок его действия. Можно написать программу модуля поддержки для отслеживания срока действия токена, записав времени, когда получения маркера и сравнение копирования с текущего времени в [SPWebService.TokenTimeout](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPWebService.TokenTimeout.aspx) .
  
    
    
Если истекшие маркер используется для создания веб-сайта SharePoint,  это исключение. Значение маркера времени ожидания по умолчанию: 24 часа. Он может осуществляться с помощью  [SPWebService.TokenTimeout](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPWebService.TokenTimeout.aspx) .
  
    
    

## <a name="elevation-of-privilege"></a>несанкционированное получение прав;
<a name="SP15_RoleInheritance_ElevationOfPrivilege"> </a>

Несанкционированное получение прав, компонент, который был добавлен в Службы Windows SharePoint Services 3.0 позволяет вам для программного выполнения действий в коде с помощью повышенного уровня прав. Метод  [SPSecurity.RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) позволяет предоставить делегата, на котором выполняется подмножество кода в контексте учетной записи с привилегиями выше, чем текущего пользователя.
  
    
    
Ниже приведен стандартного использования **RunWithElevatedPrivileges**.
  
    
    



```cs

SPSecurity.RunWithElevatedPrivileges(delegate()
{
    // Do things by assuming the permission of the "system account".
});
```

Как правило для выполнения действий в SharePoint, необходимо получить новый объект  [SPSite](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSite.aspx) , чтобы увидеть результат изменений. Например:
  
    
    



```cs

SPSecurity.RunWithElevatedPrivileges(delegate()
{
    using (SPSite site = new SPSite(web.Site.ID))
    {
       // Do things by assuming the permission of the "system account".
    }
});
```

Несмотря на то, что несанкционированное получение прав предоставляет мощные метод для управления безопасностью, его следует использовать с осторожностью. Не следует предоставлять прямой, неконтролируемые механизмы для людей с низкими привилегиями для обхода разрешения, предоставленные им.
  
    
    

> **Важные:** Если метод, переданной в [RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) включает в себя все операции записи, вызов [RunWithElevatedPrivileges](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSecurity.RunWithElevatedPrivileges.aspx) должен предшествовать вызов [SPUtility.ValidateFormDigest()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPUtility.ValidateFormDigest.aspx) или [SPWeb.ValidateFormDigest() ](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.ValidateFormDigest.aspx) .
  
    
    


## <a name="automatic-password-changes"></a>Автоматической смены пароля
<a name="SP15_RoleInheritance_AutomaticPasswordChange"> </a>

Функции изменения автоматической смены пароля позволяет обновлять и развертывание пароли без выполнения пароля вручную обновление задач в нескольких учетных записей, служб и веб-приложений. Это упрощает управление паролем в SharePoint. Чтобы определить, является ли пароль истекает срок действия и сброс пароля с помощью строки в случайном порядке длинные, криптографически строгого можно использовать функции изменения автоматической смены пароля.
  
    
    

### <a name="managed-account"></a>Управляемая учетная запись

Использование управляемых учетных записей для реализации функции изменения автоматической смены пароля. Управляемые учетные записи повысить уровень безопасности и обеспечения изоляции приложений. Управляемые учетные записи можно выполнить следующие действия.
  
    
    

- Настройка функции изменения автоматической смены пароля для развертывания пароли для всех служб в ферме.
    
  
- Настройка веб-приложения SharePoint и службы, которые выполняются на серверах приложений в ферме SharePoint, для использования разными учетными записями домена.
    
  
- Сопоставление управляемых учетных записей для различных служб и веб-приложений в ферме.
    
  
- Создание нескольких учетных записей в доменных службах Active Directory (AD DS) и регистрация каждого из этих учетных записей в SharePoint.
    
  
Можно также регистрация управляемых учетных записей и включить SharePoint для управления паролей учетных записей. Пользователи должны получать уведомления о изменения запланированных пароль и другие связанные службы, но учетные записи, используемые фермой SharePoint, веб-приложений и автоматически сбросить и развернуты в пределах фермы при необходимости, различных служб на основе настраивать расписания сброса пароля по отдельности.
  
    
    
Операции, которые можно использовать класс  [SPManagedAccount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.aspx) для выполнения относятся:
  
    
    

- Изменение пароля
    
  
- Задать расписание смены паролей
    
  
- Распространения смены пароля
    
  
- Определить, когда последнего изменения пароля
    
  
- Принудительное применение Минимальная длина пароля
    
  
Дополнительные сведения об API управляемой учетной записи можно найти по следующим ссылкам:
  
    
    

-  [SPManagedAccount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.aspx)
    
  
-  [SPManagedAccount.EventProcessingOptions](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.EventProcessingOptions.aspx)
    
  
-  [SPManagedAccount.EventType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPManagedAccount.EventType.aspx)
    
  

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15_RoleInheritance_AdditionalResources"> </a>


-  [Проверка подлинности, авторизация и безопасность в SharePoint](authentication-authorization-and-security-in-sharepoint.md)
    
  
-  [Авторизация, пользователи, группы и объектная модель в SharePoint](authorization-users-groups-and-the-object-model-in-sharepoint.md)
    
  
-  [Удостоверение, основанное на основе утверждений в SharePoint](claims-based-identity-in-sharepoint.md)
    
  
-  [Удостоверение, основанное на утверждениях и концепций в SharePoint](claims-based-identity-and-concepts-in-sharepoint.md)
    
  
-  [Настройки, администрирования и ресурсы в SharePoint](configuration-administration-and-resources-in-sharepoint.md)
    
  
