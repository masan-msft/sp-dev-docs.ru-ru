---
title: "Фильтрация по ролям безопасности для поиска в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: fbbf0cc4-e135-426a-9996-34eb954dbd5a
ms.openlocfilehash: d42bb0cbc5bf1976fd772b0ad900c5f550907d9f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="custom-security-trimming-for-search-in-sharepoint"></a>Фильтрация по ролям безопасности для поиска в SharePoint
Сведения о двух типах интерфейсов триммера безопасности, **ISecurityTrimmerPre** и **ISecurityTrimmerPost**и действия, которые необходимо выполнить, чтобы создать пользовательский триммер безопасности.
Во время выполнения запроса поиска в SharePoint выполняет фильтрацию по ролям безопасности результатов поиска, основанные на идентификатор пользователя, отправившего запрос, с помощью сведения о безопасности, полученный из компонента обхода контента.
  
    
    

Возможно, некоторые сценарии, тем не менее, в которых результаты фильтрации по ролям встроенные функции безопасности не достаточно для конкретной ситуации. В подобных ситуациях необходимо реализовать фильтрации по ролям безопасности. Поиск в SharePoint предоставляет поддержку для фильтрации по ролям безопасности через интерфейс [ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) , [ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) интерфейс и интерфейс [ISecurityTrimmer2](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmer2.aspx) (устарело) в [ Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx) пространства имен.
 **Примечание:** Настраиваемые перед триммеры не поддерживают идентификаторы безопасности Windows в списки управления доступом, только утверждений. Если какие-либо идентификатор безопасности заявляют, что возвращаются типы из настраиваемого триммера предварительной, полученные записи управления доступом в индексе кодируется как утверждение, не как ИД безопасности. Поэтому они не соответствуют удостоверения пользователя Windows, основанных на ИД безопасности.
  
    
    


## <a name="implementing-the-interfaces-for-custom-security-trimming"></a>Реализация интерфейсов для фильтрации по ролям безопасности
<a name="Implementing_the_interfaces"> </a>

Интерфейс **ISecurityTrimmerPre** выполняет вычисление предварительная фильтрацию по ролям или предварительного запроса, где переписывать поисковый запрос для добавления сведений о безопасности перед сопоставление поисковый запрос в поисковый индекс. Интерфейс **ISecurityTrimmerPost** выполняет вычисление после обрезки или после запроса, где удаляются результатов поиска, прежде чем они возвращаются пользователю.
  
    
    
Рекомендуется использовать предварительная фильтрацию по ролям для повышения производительности и общие правильность; Предварительная фильтрацию по ролям предотвращает утечки информации для уточнения данных и нажатия количество экземпляров. После trimmers можно использовать в случаях, где фильтрации по ролям безопасности непредусмотренным точно с помощью фильтров запроса; Например при наличии в зависимости от часового пользователя выдачи запроса, таких как только официальный рабочее время документы нужно отфильтровать нет на месте.
  
    
    

### <a name="implementing-the-isecuritytrimmerpre-interface"></a>Реализация интерфейса ISecurityTrimmerPre

Создание настраиваемых безопасности старые устройство обрезки для результатов поиска, необходимо создать компонентом, который интерфейс **ISecurityTrimmerPre**.
  
    
    
Интерфейс **ISecurityTrimmerPre** содержит два метода, которые необходимо реализовать: [Initialize(NameValueCollection, SearchServiceApplication)](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.Initialize.aspx) и [AddAccess(Boolean, Claims)](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.AddAccess.aspx) .
  
    
    

#### <a name="initialize-method"></a>Метод Initialize

Метод **Initialize** выполняется при устройство обрезки старые безопасности загружается в рабочий процесс, пока не будет повторно рабочий процесс не выполняет еще раз. Два параметра передаются в метод:
  
    
    

-  _staticProperties_:  [NameValueCollection](https://msdn.microsoft.com/library/System.Collections.Specialized.NameValueCollection.aspx) объект, содержащий конфигурации свойства, заданные для устройство обрезки безопасности при регистрации приложения службы поиска.
    
  
-  _searchApplication_:  [SearchServiceApplication](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.aspx) объект, который представляет приложения службы поиска.
    
  

#### <a name="addaccess-method"></a>Метод AddAccess

Метод **AddAccess** выполняется на устройство до обрезки, для каждого запроса входящих перед вычислением запрос один раз.
  
    
    
Два параметра передаются в этот метод: 
  
    
    

-  _sessionProperties_: **[T:System.Collections.Generic.IDictionary<String,Object>]** объект, который содержит свойства запроса.
    
  
-  _userIdentity_:  [IIdentity](https://msdn.microsoft.com/library/System.Security.Principal.IIdentity.aspx) объект, который содержит удостоверение пользователя.
    
  

### <a name="implementing-the-isecuritytrimmerpost-interface"></a>Реализация интерфейса ISecurityTrimmerPost

Чтобы создать пользовательский безопасности после устройство обрезки для результатов поиска, необходимо создать компонентом, который интерфейс **ISecurityTrimmerPost**.
  
    
    
Интерфейс **ISecurityTrimmerPost** содержит два метода, которые необходимо реализовать: [Initialize(NameValueCollection, SearchServiceApplication)](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.Initialize.aspx) и **CheckAccess(IList<String>, IList<String>, IDictionary<String, Object>, IIdentity)**.
  
    
    

#### <a name="initialize-method"></a>Метод Initialize

Метод **Initialize** выполняется при устройство обрезки безопасности загружается в рабочий процесс, пока не будет повторно рабочий процесс не выполняет еще раз. Два параметра передаются в метод: и
  
    
    

-  _staticProperties_:  [NameValueCollection](https://msdn.microsoft.com/library/System.Collections.Specialized.NameValueCollection.aspx) объект, содержащий свойства конфигурации, заданному для устройство обрезки безопасности при регистрации приложения службы поиска.
    
  
-  _searchApplication_:  [SearchServiceApplication](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.aspx) объект, который представляет приложения службы поиска.
    
  

#### <a name="checkaccess-method"></a>Метод CheckAccess

Метод **CheckAccess** выполняется один раз в устройство после обрезки, для каждого запроса результирующий набор, после оценки запроса.
  
    
    
Четыре параметры передаются в этот метод:
  
    
    

-  _documentUrls_: A [IList\<T\> ](http://msdn2.microsoft.com/EN-US/library/5y536ey6) объект, который содержит URL-адреса для каждого элемента контента в результатах поиска, соответствующие правила обхода контента.
    
  
-  _documentAcls_: A [IList\<T\> ](http://msdn2.microsoft.com/EN-US/library/5y536ey6) object, содержащий элемент списков управления доступом для каждого элемента контента, чьи доступа — это будет определено в реализации триммера безопасности.
    
  
-  _управляющегопользователями_: A [IDictionary\<TKey, TValue\> ](http://msdn2.microsoft.com/EN-US/library/s4ys34ea) object, содержащий контейнер временные свойств.
    
  
-  _userIdentity_: объекта  [IIdentity](https://msdn.microsoft.com/library/System.Security.Principal.IIdentity.aspx) , из которого исполняющих объектов можно получить учетные данные пользователя.
    
  
Метод **CheckAccess** возвращает [BitArray](https://msdn.microsoft.com/library/System.Collections.BitArray.aspx) объект, который представляет массив значений **true** или **false**, один для каждого URL-адреса элемента содержимого в **IList** объект, который был передан в качестве первого параметра метода. Компонент обработки запросов использует эти значения для выполнения после фильтрации по ролям безопасности результатов. Если значение массива для определенного элемента контента **true**, элемент включается в возвращаемые результаты; Если значение массива **false**, удалить элемент.
  
    
    
При реализации метода **CheckAccess** можно использовать двумя элементам данных для каждого элемента определить, следует ли возвращать **true** или **false** для элемента: удостоверение пользователя, отправившего запрос и URL-адрес элемента содержимого. Кроме того можно также передать информацию ACL настраиваемый документ от соединителя метода **CheckAccess**.
  
    
    

#### <a name="retrieving-the-user-identity-for-your-security-trimmer"></a>Получение удостоверение пользователя для вашей безопасности устройство обрезки

Удостоверение пользователя можно извлекать с текущего участника потока, как показано в следующем примере.
  
    
    

```cs

IIdentity userIdentity = System.Threading.Thread.CurrentPrincipal.Identity;
```

Также необходимо включить следующую директиву пространства имен.
  
    
    



```cs
using System.Security.Principal;
```

Идентификатор пользователя также можно получить из параметра **passedUserIdentity** метода **CheckAccess**.
  
    
    

#### <a name="passing-document-acls-from-the-connector-to-your-security-trimmers"></a>Передача ACL документа из соединительную линию в вашей trimmers безопасности

Соединитель, названия, является мост связи между SharePoint и внешней системы, на котором размещается внешних данных. При работе с помощью настраиваемых соединителей можно передать сведения списка управления Доступом документа непосредственно после триммер путем установки свойства **docaclmeta** документа. Настроенные соединители и конечные триммеры имеют одинаковый формат и интерпретации поля, вы можете использовать для передачи пользовательских данных.
  
    
    
Строки, хранящиеся в **docaclmeta** соединителем будет контактной в параметре _documentAcls_ при вызове метод **CheckAccess** устройство обрезки настраиваемые безопасности. Обычный документ ACL в свойстве **docacl** обрабатываются по ролям безопасности основные и не отображаются на устройство обрезки настраиваемые безопасности. Аналогичным образом свойство **docaclmeta** не влияет на фильтрации по ролям безопасности основные.
  
    
    

#### <a name="post-trimmers-and-their-effect-on-refiner-count-for-security-trimmers"></a>После trimmers и их влияние на количество уточнения для trimmers безопасности

При работе с после trimmers важно Обратите внимание на то, что имеется два типа таблицы результатов: **RelevantResults** и **RefinementResults**. После trimmers применяются только к найденных результатов в **RelevantResults**. Таким образом возможно, там будут уточнения, связанные с ним в текстах усеченных обращений и **RefinementResults** count может быть больше или равно **RelevantResults**. Можно решить такое поведение двумя способами:
  
    
    

- Исключение конфиденциальных уточнений панели уточнения результатов поиска в веб-части по умолчанию, чтобы утечки нет информации с помощью уточнения.
    
  
- Использование настраиваемых веб-части для отображения уточнения или результаты при использовании после trimmers таким образом, чтобы **RefinementResults** могут быть скрыты элегантно в случаях, где **RefinementResults** count превышает число **RelevantResults**.
    
  

### <a name="retrieving-individual-configuration-properties-for-your-security-trimmer"></a>Получение свойств отдельной конфигурации для вашей безопасности устройство обрезки

Можно получить доступ к отдельной конфигурации свойства, используя имя свойства, который был указан при регистрации устройство обрезки после безопасности. Например следующий код возвращает значение для настройки свойство с именем **CheckLimit**.
  
    
    

```cs
public void Initialize(NameValueCollection staticProperties, SearchServiceApplication searchApplication)
{
    if (staticProperties["CheckLimitProperty"] != null)
    {
         intCheckLimit = Convert.ToInt32(staticProperties["CheckLimitProperty"]);
    }
}
```


## <a name="deploying-the-custom-security-trimmer-component"></a>Развертывание компонента настраиваемого триммера безопасности
<a name="Deploying_the_trimmer"> </a>

После создания устройство обрезки выборочные ее необходимо развернуть в глобальный кэш на любом сервере роль запроса. Шаг 2 в  [Способ: использование пользовательского триммера безопасности для результатов поиска SharePoint Server](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md) описывает процесс развертывания устройство обрезки выборочные глобальный кэш.
  
    
    

## <a name="registering-the-custom-security-trimmer"></a>Регистрация пользовательского триммера безопасности
<a name="Registering_the_trimmer"> </a>

После trimmers для регистрации обрезки выборочные необходимо связать с определенного приложения службы поиска и правило обхода контента; для предварительного trimmers это не является обязательным.
  
    
    
Используйте командлет **SPEnterpriseSearchSecurityTrimmer**Командная консоль SharePoint зарегистрировать устройство выборочные обрезки.
  
    
    
В следующей таблице описаны параметры, которые использует командлет.
  
    
    

**Таблица 1. Параметры командлета SPEnterpriseSearchSecurityTrimmer**


|**Параметр**|**Описание**|
|:-----|:-----|
| _Приложение службы_ <br/> |Обязательно. Имя приложения службы поиска, например «приложения службы поиска».  <br/> |
| _Имя типа_ <br/> |Обязательный атрибут. Строгое имя сборки пользовательских триммеров безопасности.  <br/> |
| _RulePath_ <br/> |Обязательно для после trimmers; необязательно для предварительного trimmers. Правило обхода контента для устройство обрезки безопасности.<br/> **Примечание:** Рекомендуется использовать одно правило каждого источника контента.           |
| _id_ <br/> |Обязательный атрибут. Идентификатор триммера безопасности. Это уникальное значение. При регистрации триммера безопасности с идентификатором, который уже зарегистрирован для другого триммера безопасности, то регистрация первого триммера заменяется регистрацией второго.  <br/> |
| _properties_ <br/> |Необязательный атрибут. Пары имя/значение, указывающие свойства конфигурации. Должны иметь следующий формат:  `Name1~Value1~Name2~Value~???` <br/> |
   
Пример основные команды для регистрации устройство выборочные обрезки и пример, задающее свойства конфигурации, читайте в статье  [Способ: использование пользовательского триммера безопасности для результатов поиска SharePoint Server](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md).
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_sectrimmer_addlresources"> </a>


-  [Способ: использование пользовательского триммера безопасности для результатов поиска SharePoint Server](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md)
    
  
-  [ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx)
    
  
-  [ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx)
    
  
-  [Общие сведения о Business Connectivity Services в SharePoint](http://technet.microsoft.com/en-us/library/ee661740.aspx)
    
  
