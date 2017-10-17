---
title: "Обновление компонентов сайта с надстройкой в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: ad72f237e3c6ddb9d45c723a65c6225b02119314
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="update-add-in-web-components-in-sharepoint"></a>Обновление компонентов сайта с надстройкой в SharePoint
В этой статье рассказывается, как обновлять страницы, списки, типы контента и другие компоненты сайта надстройки в надстройке SharePoint.
 

 **Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).
 


## <a name="prerequisites-for-updating-the-add-in-web-components"></a>Компоненты, необходимые для обновления компонентов сайта надстройки
<a name="Prerequisites"> </a>

Изучите статью [Обновление надстроек SharePoint](update-sharepoint-add-ins.md) и ознакомьтесь со списком необходимых компонентов и основными понятиями, описанными в этой статье.
 

 
В этом разделе предполагается, что вы разработали и протестировали последнюю версию надстройки, как это описано в статье  [Создание и отладка новой версии в качестве новой надстройки](update-sharepoint-add-ins.md#DebugFirst).
 

 

## <a name="update-sharepoint-components-in-the-add-in-web"></a>Обновление компонентов SharePoint на сайте надстройки
<a name="UpdatingAppWeb"> </a>

Все элементы SharePoint, развернутые на сайте надстройки, содержатся в компонентах области **Web** (Интернет) в пакете надстройки, поэтому для обновления этих элементов необходимо обновить один или несколько компонентов. Этот процесс не изменился со времени выпуска SharePoint 2010 и описан в статье [Практическое руководство. Добавление элементов к существующему компоненту](http://msdn.microsoft.com/library/b007f419-e0d6-4e3a-a3ae-b8e448656d02%28Office.15%29.aspx) в пакете SDK для SharePoint 2010. Другие статьи, указанные в узле [Обновление компонентов](http://msdn.microsoft.com/library/e917f709-6491-4d50-adbe-2ab8f35da990%28Office.15%29.aspx), также могут пригодиться, но учтите, что надстройки не должны включать пользовательский код на сервере SharePoint, поэтому некоторые аспекты обновления компонентов в SharePoint 2010 не относятся к обновлению надстроек. Например, вам не удастся использовать элемент [CustomUpgradeAction](http://msdn.microsoft.com/library/16a2182e-80aa-4184-8071-8f717ee5c572%28Office.15%29.aspx) при обновлении компонента надстройки SharePoint.
 

 

### <a name="what-can-and-cannot-be-done-declaratively"></a>Действия, которые можно и которые нельзя выполнить декларативно

В случае обновления надстройки, размещенной в SharePoint, можно использовать только разметку XML. При этом возможности декларативного изменения надстройки будут ограничены. Для надстройки, размещенной на стороне поставщика, можно реализовать  [обработчик UpdatedEventEndpoint](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md), чтобы выполнить действия, которые невозможно сделать декларативно.
 

 
Добавлять компоненты в надстройку просто. Любой компонент, который можно включить в надстройку, можно добавить также в обновление. (Дополнительные сведения о компонентах, которые могут входить в надстройку, можно найти в статье  [Типы компонентов SharePoint, которые могут находиться в надстройке для SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#TypesOfSPComponentsInApps).) Но если вы хотите изменить существующий компонент декларативно, учтите указанные ниже сведения. 
 

 

- Тип данных поля (столбца) списка или типа контента в любом случае невозможно изменить после первоначального развертывания. В частности, не меняйте этот тип данных при обновлении надстройки ( *даже программно*  ). В качестве альтернативного решения вы можете добавить новое поле. Если надстройка содержит пользовательские формы для создания, редактирования или просмотра элементов, не забудьте внести в них соответствующие изменения. Например, добавьте элемент пользовательского интерфейса для нового поля и удалите его для старого. (В надстройке, размещенной на стороне поставщика, можно программным путем переместить данные из старого поля в новое, а затем удалить старое.)
    
 
- Вам не удастся удалить списки, экземпляры списков, типы контента или поля в разметке обновления.
    
 
- Вам не удастся удалить файлы с сайта надстройки в разметке обновления. Тем не менее вы можете изменить содержимое любого файла.
    
 
- Вам не удастся использовать элементы **CustomUpgradeAction** и **MapFile** при обновлении надстройки SharePoint, хотя они могут быть доступными в IntelliSense для Visual Studio.
    
 

### <a name="update-the-add-in-web-for-the-first-time"></a>Первое обновление сайта надстройки

В этом разделе описано, как добавлять или обновлять типы контента, списки, файлы и другие компоненты SharePoint на сайте надстройки. Чтобы было проще, предполагается, что все компоненты входят в один компонент на сайте надстройки. Но этот сайт может иметь несколько таких компонентов, и за один раз можно обновить несколько таких компонентов.
 

 
Инструменты разработчика Microsoft Office для Visual Studio ориентированы на создание надстроек, поэтому поведение этих средств, заданное по умолчанию, не всегда оптимально при обновлении надстройки. Для большего контроля над процессом сначала отключите конструктор компонентов, выполнив описанные ниже действия, чтобы можно было непосредственно изменять неотформатированный XML компонента. 
 

 

### <a name="to-edit-the-feature-xml"></a>Изменение XML компонента


1. В **обозревателе решений** откройте файл _{Имя_Компонента}_.features. Он откроется в редакторе компонентов.
    
 
2. Откройте вкладку **Манифест** и разверните пункт **Параметры правки**.
    
 
3. Выберите пункт **Перезаписать созданный XML и редактировать манифест в редакторе XML**.
    
 
4. Когда отобразится соответствующий запрос, нажмите кнопку **Да**, чтобы отключить конструктор.
    
 
5. В открывшемся представлении выберите пункт **Редактирование манифеста в XML-редакторе**. Откроется файл _{Имя_Компонента}_.Template.xml. 
    
    **Открытие XML-редактора компонентов**

 

  ![Действия, которые необходимо выполнить, чтобы открыть XML-редактор компонентов](../images/UpdateAppOpenFeatureXML.png)
 

 

 

 **Внимание!** Не добавляйте комментарии "<!-- -->" в файл _{Имя_Компонента}_.features. Комментарии не поддерживаются инфраструктурой обновления, и вам не удастся выполнить обновление, если в файле есть комментарии. Комментарии используются в примерах разметки в этой статье, только чтобы показать вам, куда следует поместить разметку.
 

Чтобы обновить компонент сайта надстройки, выполните указанные ниже действия.
 

 

### <a name="to-update-the-add-in-web-feature-the-first-time"></a>Первое обновление компонента сайта надстройки


1. Увеличьте на единицу значение атрибута **Version** (Версия) для элемента [Feature](http://msdn.microsoft.com/library/265cd648-1a7e-410f-a1d7-0da8c64b4006%28Office.15%29.aspx) (Компонент), если пакет Инструменты разработчика Office для Visual Studio еще не сделал это при увеличении номера версии в манифесте надстройки. (Пакет Инструменты разработчика Office для Visual Studio делает это не в каждом сценарии, поэтому необходимо выполнять соответствующую проверку.) Вам следует использовать тот же номер версии, что и для надстройки. Вам даже следует рассмотреть вопрос об увеличении версии компонента при обновлении других компонентов надстройки, но не самого компонента сайта надстройки. Логикой элемента [VersionRange](http://msdn.microsoft.com/library/cd715e38-6ec3-43b2-8007-6d0ed8865d91%28Office.15%29.aspx) (который рассматривается в разделе [Последующие обновления сайта надстройки](#SubsequentUpgrades)) легче управлять, если версия надстройки и версия компонента всегда одинаковы. 
    
 
2. Никогда и ничего не удаляйте в разделе [ElementManifests](http://msdn.microsoft.com/library/d8d4db7e-2bc2-40c6-958b-d5683bdee87a%28Office.15%29.aspx) файла.
    
 
3. Добавьте указанные ниже элементы в файл (если они еще не добавлены). 
    
      - Дочерний элемент  [UpgradeActions](http://msdn.microsoft.com/library/5af24ac1-a290-454d-b32b-bc7f7a4634f0%28Office.15%29.aspx) в элемент **Feature**.  *Не*  добавляйте атрибуты **ReceiverAssembly** или **ReceiverClass** в элемент. Они не используются при обновлении надстройки SharePoint. Эти атрибуты ссылаются на настраиваемую сборку, неподдерживаемую в надстройках SharePoint. Если вы включите настраиваемую сборку в надстройку, SharePoint ее не установит.
    
 
  - Дочерний элемент **VersionRange** в элементе **UpgradedActions**. Не добавляйте атрибуты **BeginVersion** или **EndVersion** в элемент. Это бесполезно, когда надстройка обновляется впервые. Об использовании этих элементов будет рассказано в разделе [Последующие обновления сайта надстройки](#SubsequentUpgrades).
    
 
  - Дочерний элемент [ApplyElementManifests](http://msdn.microsoft.com/library/c087a0c3-1e27-4034-b4da-e025991454d6%28Office.15%29.aspx) в элементе **VersionRange**.
    
 

    На данный момент файл должен выглядеть приблизительно так, как показано в примере ниже.
    
     **Важно!** Возможно, в качестве примера пакет Инструменты разработчика Office для Visual Studio уже добавил указанную выше разметку и скопировал некоторые элементы из раздела **ElementManifests** в раздел **ApplyElementManifests**. *Удалите их*. Не исключено, что вам придется в дальнейшем возвращать некоторые из них обратно. Но намного легче и безопаснее начать работу с пустого раздела **ApplyElementManifests**. Лишние записи для компонентов, которые не изменялись, могут иметь плохие последствия. Например, длительность процесса обновления может увеличиться настолько, что будет превышено время ожидания, и обновление завершится ошибкой.



```XML
  <Feature <!-- Some attributes omitted --> 
               Version="2.0.0.0">
  <ElementManifests>
    <!-- ElementManifest elements omitted -->
  </ElementManifests>
  <UpgradeActions>
   <VersionRange>
     <ApplyElementManifests>
       
     </ApplyElementManifests>
   </VersionRange>
  </UpgradeActions>
</Feature>
```


### <a name="to-add-components-to-the-add-in"></a>Добавление элементов в надстройку


1. Добавьте все новые элементы в компонент точно так же, как при создании проекта надстройки SharePoint.
    
 
2. Когда вы добавляете компонент типа, который отсутствовал в предыдущей версии надстройки (например, добавляете в надстройку список, которого раньше не было), пакет Инструменты разработчика Office для Visual Studio добавляет файл elements.xml в проект. Это манифест элементов для компонента. К этому файлу следует добавить номер новой версии надстройки (например, elements.2.0.0.0.xml). Это может быть удобно при устранении неполадок. Не забудьте внести изменения в **обозревателе решений**, чтобы ссылки на файл (например, в CSPROJ-файле и XML компонента) тоже изменились.
    
 
3. Для каждого нового манифеста элементов добавьте дочерний элемент  [ElementManifest](http://msdn.microsoft.com/library/5a6a2865-5d31-45a2-a402-6da6e0f5567a%28Office.15%29.aspx) в элементы **ElementManifests** и **ApplyElementManifests** XML компонента. (Тот же элемент **ElementManifest** в обоих случаях.) Атрибут **Location** должен указывать на относительный путь к файлу elements.2.0.0.0.xml. Например, если вы добавили список с именем MyCustomList, элемент **ElementManifest** будет выглядеть следующим образом.
    
```XML
  <ElementManifest Location="MyCustomList\elements.2.0.0.0.xml" />
```

4. Некоторые виды компонентов добавляют к проекту файлы. Например, при добавлении списка создается файл schema.xml. А когда вы добавляете страницу, создается файл подкачки. Добавьте дочерний элемент  [ElementFile](http://msdn.microsoft.com/library/bd43638e-8f18-4a0d-b122-1c055f97aa71%28Office.15%29.aspx) в элемент **ElementManifests** для каждого такого файла. (Не добавляйте его в элемент **ApplyElementManifests**.) Атрибут **Location** должен указывать на относительный путь файла. Например, если вы добавили список, элемент **ElementFile** файла schema.xml будет выглядеть следующим образом.
    
```XML
  <ElementFile Location="MyCustomList\Schema.xml" />
```

5. При добавлении другого элемента типа, который уже использовался в предыдущей версии надстройки, пакет Инструменты разработчика Office для Visual Studio может добавить ссылку на новый элемент в существующий манифест элементов, а не создавать новый. Например, чтобы добавить страницу на сайт надстройки, обычно нужно щелкнуть правой кнопкой мыши узел **Страницы** в **обозревателе решений**, а затем последовательно выбрать пункты **Добавить | Новый элемент | Страница | Добавить**. Вместо того чтобы создавать новый манифест элементов, пакет Инструменты разработчика Office для Visual Studio добавит новый элемент **File** (Файл) в модуль **Pages** (Страницы) в существующий файл манифеста элементов (обычно он называется elements.xml).
    
    Это нежелательное действие. По возможности при обновлении надстройки не изменяйте существующие файлы манифеста элементов для предыдущих версий надстройки. Как правило, новые элементы должны находиться в новых файлах манифеста элементов (на которые ссылается элемент **ApplyElementManifests** XML компонента). (Есть несколько исключений, и они описаны ниже.) Например, чтобы добавить новую страницу, выполните указанные ниже действия.
    
      1. Создайте модуль с именем Pages.2.0.0.0.
    
 
  2. Удалите из него файл sample.txt, который Инструменты разработчика Office для Visual Studio добавляют автоматически.
    
 
  3. Переименуйте манифесты элементов в новом модуле на elements.2.0.0.0.xml.
    
 
  4. Щелкните правой кнопкой мыши модуль **Pages.2.0.0.0** и последовательно выберите пункты **Добавить | Новый элемент | Страница | Добавить**. Будет создана страница, на которую будет ссылаться манифест элементов для модуля **Pages.2.0.0.0**, а не **Pages**.
    
 
  5. Убедитесь, что имеется элемент **ElementsFile** для новой страницы в элементе **ElementManifests** XML компонента и элемент **ElementManifest** для файла elements.2.0.0.0.xml в разделах **ElementManifests** и **ApplyElementManifests**.
    
 

    В любой ситуации, когда пакет Инструменты разработчика Office для Visual Studio изменил существующий манифест элементов, можно использовать еще один вариант: вручную создать файл elements.2.0.0.0.xml и переместить в него разметку, добавленную в старый манифест. (При желании вы можете поместить новый манифест в тот же узел в **обозревателе решений**, в котором находится старый манифест.)
    
 
6. Если вы добавляете поле в тип контента компонента, добавьте элемент  [AddContentTypeField](http://msdn.microsoft.com/library/cb04a3ac-f41a-4ffe-aaa1-d4bf3fb6347d%28Office.15%29.aspx) в раздел **VersionRange**. Убедитесь, что вы присвоили правильные значения атрибутам **ContentTypeId** и **FieldId**. С помощью атрибута **PushDown** укажите, будет ли добавлено новое поле в какой-либо производный тип контента (необязательно). Ниже приведен пример.
    
```XML
  <VersionRange>
  <AddContentTypeField 
    ContentTypeId="0x0101000728167cd9c94899925ba69c4af6743e"
    FieldId="{CCDD361F-A3FB-40D8-A272-3A3C858F4116}"
    PushDown="TRUE" />
  <!-- Other child elements of VersionRange -->
</VersionRange>
```


### <a name="to-modify-existing-components-of-the-add-in"></a>Изменение существующих компонентов надстройки


1. Если вы изменили файл, на который имеется ссылка в файле манифеста элементов (например, файл Default.aspx), вам вообще не нужно изменять элемент **ElementFile** для файла. Тем не менее необходимо сообщить инфраструктуре обновления, что следует заменить старую версию файла на новую. Это можно сделать, добавив элемент **ElementManifest** для модуля в раздел **ApplyElementManifests**. Так как в разделе **ElementManifests** уже существует такой элемент, иногда можно просто скопировать (а не переместить) его в **ApplyElementManifests**. Это рекомендуется делать, только если были изменены все файлы, на которые ссылается манифест. Обычно не нужно заменять неизмененный файл его копией, так как в ряде сценариев это может иметь плохие последствия. Например, если страница настроена так, что пользователи могут изменять ее, то в результате замены внесенные изменения могут быть удалены. Если вы изменили страницу, вам придется учитывать эти последствия, но не нужно без веской причины доставлять неудобства пользователям.
    
    Чтобы удостовериться, что заменены только измененные файлы модуля, создайте еще один манифест элементов для модуля, который будет ссылаться только на измененные файлы, и примените второй манифест в **ApplyElementManifests**, выполнив указанные ниже действия.
    
      1. Щелкните правой кнопкой мыши узел модуля в **обозревателе решений** и добавьте XML-файл (не страницу) с именем elements.2.0.0.0.xml.
    
 
  2.  Выберите новый файл в области **Обозреватель решений**, чтобы его область свойств стала видимой, и измените свойство **Deployment Type** на **ElementManifest**. Это обязательно нужно сделать, чтобы обработка файла с помощью Инструменты разработчика Office для Visual Studio выполнялась должным образом.
    
 
  3. Скопируйте содержимое исходного манифеста в новый и удалите из нового манифеста все элементы меню  [Файл](http://msdn.microsoft.com/library/c270e4ce-8110-4da7-b0e7-c223604bfce7%28Office.15%29.aspx), соответствующие **неизмененным** файлам.
    
 
  4. Добавьте элемент **ElementManifest** в раздел **ApplyElementManifests**, который ссылается на новый файл манифеста, как показано в примере ниже.
    
```XML
  <ElementManifest Location="Pages\elements.2.0.0.0.xml" />
```


     **Note**   Do not delete the original manifest. The Feature XML is using both of the old and new ones. Do not copy any **ElementFile** elements from the **ElementManifests** section to the **ApplyElementManifests** section even if the file that is referenced in the **ElementFile** has been changed.
2. Откройте каждый файл манифеста элементов, на который имеются ссылки в разделе **ApplyElementManifests**, и удостоверьтесь, что у всех элементов [File](http://msdn.microsoft.com/library/c270e4ce-8110-4da7-b0e7-c223604bfce7%28Office.15%29.aspx) (Файл) есть атрибут **ReplaceContents** со значением **TRUE** (Истина). Ниже приведен пример. Возможно, пакет Инструменты разработчика Office для Visual Studio уже сделал это, но вам следует убедиться в этом. Проверьте даже манифесты элементов для предыдущих версий надстройки. Это один из хороших способов изменения существующего файла манифеста элементов.
    
```XML
  <Module Name="Pages">
  <File Path="Pages\Default.aspx" Url="Pages/Default.aspx" ReplaceContent="TRUE" />
</Module>
```

3. В страницы могут быть встроены веб-части, как описано в статье [Добавление веб-части на страницу сайта надстройки](include-a-web-part-in-a-webpage-on-the-add-in-web.md). Если вы изменяете страницу со встроенной веб-частью (или изменяете свойства веб-части), потребуется выполнить дополнительное действие: добавить на страницу указанную ниже разметку, чтобы служба SharePoint не добавила вторую копию веб-части на страницу. Разметку необходимо добавить к элементу **asp:Content** с идентификатором `PlaceHolderAdditionalPageHead`. (Возможно, при создании страницы пакет Инструменты разработчика Office для Visual Studio уже добавил ее, но вам нужно убедиться в этом.)
    
```XML
  <meta name="WebPartPageExpansion" content="full" />
```


     **Note**   If the page was configured to allow users to customize it, then this markup has the side effect of removing those customizations. Users will have to repeat them. If the Web Part was added to the page following the guidance in [Include a Web Part in a webpage on the add-in web](include-a-web-part-in-a-webpage-on-the-add-in-web.md), then the Web Part markup is in the elements manifest, so changing the Web Part's properties is an exception to the general rule that you should not edit an element manifest file as part of an add-in update. 
4. Вместо того чтобы изменять страницу, вы можете использовать перенаправление на новую страницу, выполнив указанные ниже действия. 
    
      1. Создайте страницу и настройте для нее разметку обновления, как описано выше в разделе **Добавление компонентов в надстройку**.
    
 
  2. Откройте старую страницу и удалите всю разметку из элемента **asp:Content** с идентификатором `PlaceHolderAdditionalPageHead`. 
    
 
  3. Добавьте указанную ниже разметку в элемент **asp:Content** и замените путь _{RelativePathToNewPageFile}_ на новый путь и имя файла. Этот сценарий перенаправит браузер на новую страницу и укажет параметры запроса. Кроме того, он исключит старую страницу из истории браузера.
    
```
  <script type="text/javascript">
        var queryString = window.location.search.substring(1);
        window.location.replace("{RelativePathToNewPageFile}" + "?" + queryString);
</script>
```

  4. Удалите все остальные элементы **asp:Content** на странице.
    
 
  5. Если вы заменяете начальную страницу надстройки, то измените элемент **StartPage** манифеста надстройки так, чтобы он указывал на новую страницу.
    
 
5. Если сайт надстройки содержит компонент **CustomAction** или **ClientWebPart**, и вы изменяете его при обновлении, тогда вам потребуется изменить манифест элементов, так как в нем определены эти компоненты. Это исключение из общего правила, которое не разрешает изменять манифест элементов предыдущей версии надстройки при ее обновлении. Кроме того, необходимо скопировать (не переместить) элемент **ElementManifest** из раздела **ElementManifests** в раздел **ApplyElementManifests**.
    
 

#### <a name="example-of-feature-xml-for-upgrading-an-add-in-the-first-time"></a>Пример XML компонента для первого обновления надстройки

Ниже показан пример полного файла _{Имя_Компонента}_.Template.xml для первого обновления надстройки. В этом примере обновленная надстройка включает измененный файл Default.aspx, на который имеются ссылки в файле `Pages\Elements.xml`, и она развертывает три новых файла jQuery, на каждый из которых есть ссылка в файле `Scripts\Elements.xml`. Обратите внимание, что все элементы **ElementFile** перемещаются в раздел **ElementManifests**. Кроме того, обратите внимание, каким образом выполняется копирование (не перенос) `<ElementManifest Location="Pages\Elements.xml" />` из раздела **ElementManifests** в раздел **ApplyElementManifests**.
 

 

```XML
<Feature xmlns="http://schemas.microsoft.com/sharepoint/" Title="MyApp Feature1" 
      Description="SharePoint Add-in Feature" Id="85d309a8-107e-4a7d-b3a2-51341d3b11ff" 
      Scope="Web" Version="2.0.0.0">
  <ElementManifests>
    <ElementFile Location="Pages\Default.aspx" />
    <ElementManifest Location="Pages\Elements.xml" />
    <ElementFile Location="Content\App.css" />
    <ElementManifest Location="Content\Elements.xml" />
    <ElementFile Location="Images\AppIcon.png" />
    <ElementManifest Location="Images\Elements.xml" />
    <ElementFile Location="Scripts\jquery-3.0.0.intellisense.js" />
    <ElementFile Location="Scripts\jquery-3.0.0.js" />
    <ElementFile Location="Scripts\jquery-3.0.0.min.js" />
  </ElementManifests> 
  <UpgradeActions>
      <VersionRange>      
        <ApplyElementManifests>
          <ElementManifest Location="Pages\Elements.xml" />
          <ElementManifest Location="Scripts\elements.2.0.0.0.xml" />
        </ApplyElementManifests>
      </VersionRange>
  </UpgradeActions>
</Feature>

```


### <a name="subsequent-updates-of-the-add-in-web"></a>Последующие обновления сайта надстройки
<a name="SubsequentUpgrades"> </a>

Когда вы обновляете надстройку SharePoint второй (или третий и т. д.) раз, следует учитывать, что некоторые из ваших клиентов, возможно, не установили предыдущие обновления. Таким образом, если пользователь отвечает на сообщение "доступно обновление" после развертывания вашего последнего обновления в каталоге надстроек организации или в Магазине Office, экземпляр надстройки пользователя можно обновить с использованием нескольких версий в рамках единого процесса обновления. По большей части это именно то, что нужно: выполнить обновление каждой более ранней версии надстройки до последней версии. Тем не менее вам не всегда нужно, чтобы каждое действие обновления компонента сайта надстройки повторялось для каждого экземпляра надстройки. Существует ряд действий обновления, которые не должны происходить несколько раз в конкретном экземпляре надстройки. Например, если вы добавляете поле к типу контента в одном обновлении, вам не нужно добавлять его снова в следующем обновлении. В процедуре ниже показано, как использовать элемент **VersionRange** для управления действиями обновления в зависимости от версии обновляемого компонента.
 

 

### <a name="to-change-the-add-in-web-feature-on-later-updates"></a>Изменение компонента сайта надстройки в более поздних обновлениях


1. Откройте файл _Имя_Компонента_.Template.xml для редактирования, как описано в разделе **Изменение XML компонента** ранее в этой статье, и увеличьте на единицу значение атрибута **Version** (Версия) элемента [Feature](http://msdn.microsoft.com/library/265cd648-1a7e-410f-a1d7-0da8c64b4006%28Office.15%29.aspx) (Компонент). Для компонента следует использовать тот же номер версии, что и для надстройки.
    
    В рамках данного примера предположим, что вы ранее обновили надстройку с версии 1.0.0.0 до версии 2.0.0.0, и теперь обновляете ее до версии 3.0.0.0. Для этого присвойте атрибуту **Version** (Версия) значение 3.0.0.0.
    
 
2. Добавьте новый элемент **VersionRange** под всеми существующими элементами **VersionRange**. *Не* добавляйте атрибут **BeginVersion** или **EndVersion** в этот элемент.
    
 
3. Присвойте элементу **VersionRange** необходимое значение, как описано в разделе **Первое обновление компонента сайта надстройки** этой статьи, чтобы учесть изменения обновленной версии компонента. При этом считайте, что используется не раздел **ApplyElementManifests**, а дочерний элемент **ApplyElementManifests** недавно добавленного элемента **VersionRange**, т. е. *самый нижний* элемент в XML-файле компонента.
    
 
4. Перейдите к предыдущему элементу **VersionRange**, который вы добавили при последнем обновлении надстройки (с версии 1.0.0.0 до версии 2.0.0.0 в данном примере). Добавьте к этому элементу атрибут **EndVersion**. Вам нужно, чтобы обновления в этом элементе **VersionRange** были применены к любым версиям надстройки, к которым они еще не были применены (версия 1.0.0.0). При этом важно не применять такие обновления повторно к версиям, к которым они уже были применены (версия 2.0.0.0). Значение **EndVersion** — *исключительное*, поэтому задайте его для самой ранней версии, к которой вы *не* хотите применять обновления. В данном примере вы зададите для этого параметра значение 2.0.0.0. Теперь ваш файл должен выглядеть приблизительно так, как показано ниже.
    
```XML
  <Feature <!-- Some attributes omitted --> 
               Version="3.0.0.0">
  <ElementManifests>
    <!-- ElementManifest elements omitted -->
  </ElementManifests>
  <UpgradeActions>
    <VersionRange EndVersion="2.0.0.0">
      <!--  Child elements for upgrade from 1.0.0.0 to 2.0.0.0 go here. -->
    </VersionRange>
   <VersionRange>
      <!--  Child elements for upgrade from 2.0.0.0 to 3.0.0.0 go here. -->
   </VersionRange>
  </UpgradeActions>
</Feature>
```


    Each time that you upgrade the Feature, follow the same pattern. Add a new  **VersionRange** for the latest update actions. Then add an **EndVersion** element to the *previous*  **VersionRange** element and set it to the previous version number. In the continuing example, the file would resemble the following for the update from 3.0.0.0 to 4.0.0.0.
    


```XML
  <Feature <!-- Some attributes omitted --> 
               Version="4.0.0.0">
  <ElementManifests>
    <!-- Child elements omitted -->
  </ElementManifests>
  <UpgradeActions>
    <VersionRange EndVersion="2.0.0.0">
       <!-- Child elements for upgrade from 1.0.0.0 to 2.0.0.0 go here. -->
    </VersionRange>
    <VersionRange EndVersion="3.0.0.0">
       <!-- Child elements for upgrade from 2.0.0.0 to 3.0.0.0 go here. -->
    </VersionRange>
    <VersionRange>
       <!-- Child elements for upgrade from 3.0.0.0 to 4.0.0.0 go here. -->
    </VersionRange>
  </UpgradeActions>
</Feature>
```


    Notice that the most recent  **VersionRange** element has no **BeginVersion** or **EndVersion** attributes. This ensures that the upgrade actions that go into this **VersionRange** element are applied to all previous versions of the Feature, which is what you want because all the latest changes are referenced in this **VersionRange**, and none of them have already occurred for any instance of the Feature.
    
    Notice also that the  **BeginVersion** attribute is not used in any of the **VersionRange**s. This is because the default value for the  **BeginVersion** attribute is 0.0.0.0, and that is the value that you want because you want all upgrade actions applied to every instance of the add-in that is earlier than the version that is specified in the **EndVersion** attribute.
    
     **Important**   The **VersionRange** element determines only which versions of the Feature the upgrades are applied to. It does not determine which versions of the add-in get a notification that an update is available???the notification is triggered only by the add-in version number. Within 24 hours of a new version of the add-in being available in the organization's add-in catalog or the Office Store, every installed instance of the add-in, regardless of version, has the notification that an update is available appear on its tile in the **Site Contents** page. The **VersionRange** does not affect the new version number of the newly upgraded Feature or the newly updated add-in. Those two numbers are always changed to the latest version number, regardless of what version range the Feature was in before the upgrade. This provides another good reason to avoid using a **BeginVersion** attribute. The **BeginVersion** attribute can be used to block some upgrade actions from ever occurring on some add-in instances. But it cannot block the Feature or add-in versions from being raised to the latest version. So the use of a **BeginVersion** attribute could create a situation in which two instances of your add-in could have the same add-in version number and the same add-in web Feature version number, but have different components in their add-in webs.

## <a name="verify-deployment-of-add-in-web-components"></a>Проверка развертывания веб-компонентов надстройки
<a name="VerifyDeployAppWebComp"> </a>

Выполните указанные ниже действия, чтобы проверить развертывание компонента сайта надстройки и его элементов.
 

 

### <a name="to-verify-the-provisioning-of-the-add-in-web"></a>Проверка подготовки сайта надстройки


1. Откройте страницу **Параметры сайта** на хост-сайте. В разделе **Администрирование семейства веб-сайтов** выберите ссылку **Иерархия сайтов**.
    
 
2. На странице **Иерархия сайтов** в списке отобразится URL-адрес сайта надстройки. Не запускайте его. Вместо этого скопируйте URL-адрес и используйте его при выполнении дальнейших действий.
    
 
3. Перейдите по адресу _URL-адрес_веб-приложения_/_layouts/15/ManageFeatures.aspx и когда откроется страница **Компоненты сайта**, убедитесь, что компонент присутствует в упорядоченном по алфавиту списке компонентов и имеет состояние **Активен**. 
    
 
4. Если компонент сайта надстройки включает настраиваемые столбцы сайта, перейдите по адресу _URL-адрес_веб-приложения_/_layouts/15/mngfield.aspx и на открывшейся странице **Столбцы сайта** убедитесь, что новые настраиваемые столбцы сайта включены в список.
    
 
5. Если в компонент сайта надстройки включены какие-либо настраиваемые типы контента, перейдите по адресу _URL-адрес_веб-приложения_/_layouts/15/mngctype.aspx и на открывшейся странице **Типы контента сайта** убедитесь, что новые типы контента включены в список.
    
 
6. Для каждого настраиваемого типа контента и каждого типа контента, в который вы добавили столбец, щелкните ссылку для данного типа. На открывшейся странице **Тип контента сайта** убедитесь, что в типе контента есть необходимые столбцы сайта.
    
 
7. Если в компонент сайта надстройки включены какие-либо экземпляры списка, перейдите по адресу _URL-адрес_веб-приложения_/layouts/15/mcontent.aspx и на открывшейся странице **Библиотеки и списки сайта** убедитесь в наличии ссылки **Настроить <имя_списка>** для каждого настраиваемого экземпляра списка.
    
 
8. Для каждого из этих настраиваемых экземпляров списка щелкните ссылку **Настроить <имя_списка>** и на странице параметров списка убедитесь, что в списке есть необходимые типы контента и столбцы.
    
     **Примечание.** Если на странице нет раздела **Типы контента**, вам необходимо включить управление типами контента. Щелкните ссылку **Дополнительные параметры** и на странице дополнительных параметров включите управление типами контента, а затем нажмите кнопку **ОК**. Вы вернетесь на предыдущую страницу, на которой теперь будет отображаться список раздела **Типы контента**.
9. В верхней части страницы находится **веб-адрес** списка. Если вы включили примеры элементов в свое определение экземпляров списка, скопируйте адрес и вставьте его в адресную строку браузера, а затем перейдите к списку. Убедитесь, что в списке присутствуют созданные вами примеры элементов.
    
 

## <a name="next-steps"></a>Дальнейшие действия
<a name="Next"> </a>

Вернитесь к разделу  [Основные действия при обновлении надстройки](update-sharepoint-add-ins.md#MajorAppUpgradeSteps) или перейдите непосредственно к одной из следующих статей, чтобы узнать, как обновить следующий важный компонент надстройки SharePoint.
 

 

-  [Обновление компонентов хост-сайта в SharePoint](update-host-web-components-in-sharepoint.md)
    
 
-  [Создание обработчика событий обновления в надстройках SharePoint](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md)
    
 
-  [Обновление удаленных компонентов в надстройках SharePoint](update-remote-components-in-sharepoint-add-ins.md) 
    
 

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Обновление надстроек SharePoint](update-sharepoint-add-ins.md)
    
 
-  [Практическое руководство. Добавление элементов к существующему компоненту](http://msdn.microsoft.com/library/b007f419-e0d6-4e3a-a3ae-b8e448656d02%28Office.15%29.aspx) в пакете средств разработки программного обеспечения (SDK) Microsoft SharePoint 2010.
    
 
-  [Обновление компонентов](http://msdn.microsoft.com/library/e917f709-6491-4d50-adbe-2ab8f35da990%28Office.15%29.aspx) в пакете средств разработки программного обеспечения (SDK) Microsoft SharePoint 2010.
    
 

