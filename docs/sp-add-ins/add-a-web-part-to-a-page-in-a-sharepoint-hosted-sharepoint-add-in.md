# <a name="add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in"></a>Добавление веб-части на страницу в надстройках SharePoint, размещаемых в SharePoint
Узнайте, как добавлять веб-части на страницу в надстройках SharePoint.
 

 **Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 

Эта пятая часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых в SharePoint. Для начала следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и предыдущими статьями из этой серии:
 

-  [Знакомство с созданием надстроек SharePoint с размещением в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 
-  [Развертывание и установка размещаемых в SharePoint надстроек SharePoint](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [Добавление настраиваемых столбцов в надстройки, размещенные в SharePoint](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in)
    
 
-  [Добавление настраиваемого типа контента в надстройки, размещенные в SharePoint](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in)
    
 

 **Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых в SharePoint, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с данной статьей. Кроме того, вы можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforeWebPart.sln.
 

В этой статье описывается добавление веб-части на страницу по умолчанию в надстройке SharePoint "Employee Orientation" (Обучение сотрудников).
 

## <a name="add-a-web-part-to-a-page"></a>Добавление веб-части на страницу


 

 

1. В **обозревателе решений** откройте файл Default.aspx. 
    
 
2. Мы добавим на страницу веб-часть представления списка, в которой отображается список "New Employees in Seattle" (Новые сотрудники в Сиэтле), поэтому нам больше не требуется ссылка на страницу соответствующего представления. Удалите элемент **<asp:HyperLink>** из элемента **<asp:Content>**, где для параметра **ContentPlaceHolderId** задано значение `PlaceHolderMain`. 
    
 
3. Добавьте в элемент **<asp:Content>** приведенный ниже параметр **WebPartZone**. 
    
```XML
  <WebPartPages:WebPartZone runat="server" FrameType="TitleBarOnly" 
      ID="HomePage1" Title="loc:full" />

```

4. Сохраните и закройте файл.
    
 
5. В **обозревателе решений** откройте файл elements.xml страницы в узле **Страницы**.
    
 
6. Если элемент **File** является самозакрывающимся, удалите из него символ "/" и добавьте закрывающий тег `</File>`.
    
 
7. В элементе **File** добавьте дочерний элемент **AllUsersWebPart** и задайте для его свойства **WebPartZoneID** значение идентификатора зоны веб-частей, созданной на странице. Теперь содержимое файла должно выглядеть так, как показано ниже. Эта часть кода указывает среде SharePoint, что необходимо вставить объект **AllUsersWebPart** в зону веб-частей с именем HomePage1.
    
```
  <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <Module Name="Pages">
    <File Path="Pages\Default.aspx" Url="Pages/Default.aspx" ReplaceContent="TRUE" >
      <AllUsersWebPart WebPartZoneID="HomePage1" WebPartOrder="1">

      </AllUsersWebPart>
    </File>
  </Module>
</Elements>

```

8. Добавьте элемент **CDATA** в качестве дочернего для элемента **AllUsersWebPart**. Затем добавьте элемент **webParts** в качестве дочернего для элемента **CDATA**, как в приведенной ниже части кода. 
    
```
  <AllUsersWebPart WebPartZoneID="HomePage1" WebPartOrder="1">
  <![CDATA[
    <webParts>

    </webParts>
  ]]>
</AllUsersWebPart>
```

9. Добавьте приведенную ниже часть кода, заключенную в тег **webPart**, в элемент **webParts** как дочерний элемент. Эта часть кода добавляет объект **XsltListViewWebPart** и сообщает веб-части, что требуется показать список "New Employees in Seattle" (Новые сотрудники в Сиэтле). Обратите внимание, что для нового свойства **ViewContentTypeId** задано значение "0x", а не фактический идентификатор типа контента theNewEmployee.
    
```
  
  <webPart xmlns="http://schemas.microsoft.com/WebPart/v3">
    <metaData>
      <type name="Microsoft.SharePoint.WebPartPages.XsltListViewWebPart, 
                   Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, 
                   PublicKeyToken=71e9bce111e9429c" />
    </metaData>
    <data>
      <properties>
        <property name="ListUrl">Lists/NewEmployeesInSeattle</property>
        <property name="IsIncluded">True</property>
        <property name="NoDefaultStyle">True</property>
        <property name="Title">New Employees in Seattle</property>
        <property name="PageType">PAGE_NORMALVIEW</property>
        <property name="Default">False</property>
        <property name="ViewContentTypeId">0x</property>
      </properties>
    </data>
  </webPart>
```


## <a name="run-and-test-the-add-in"></a>Запуск и тестирование надстройки


 

 

1. Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Visual Studio выполнит временную установку надстройки на тестовом сайте SharePoint и сразу же запустит ее. 
    
 
2. Когда откроется страница надстройки по умолчанию, на ней будет отображаться веб-часть представления списка. 
    
    **Страница по умолчанию с веб-частью представления списка**

 

     ![Страница надстройки по умолчанию со списком "New Employees in Seattle" (Новые сотрудники в Сиэтле), отображаемым в веб-части.](../../images/31e8e4b1-e2e6-416b-b360-9979a1f16fc7.PNG)
 

    
    
 
3. Попробуйте добавлять к списку новые элементы и редактировать существующие.
    
 
4. Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.
    
 
5. Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуем отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.
    
 

## 
<a name="Nextsteps"> </a>

В следующей статье этой серии, [Добавление рабочего процесса к надстройке, размещенной в SharePoint](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in), описано добавление рабочего процесса к надстройке SharePoint.
 

 

