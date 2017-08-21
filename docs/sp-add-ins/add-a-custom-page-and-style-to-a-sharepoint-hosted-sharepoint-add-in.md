


# <a name="add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in"></a>Добавление настраиваемых страниц и стилей в надстройки, размещенные в SharePoint
Узнайте, как включать настраиваемые страницы и CSS-файлы в надстройки SharePoint.
 

 **Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 

Эта седьмая часть серии статей, посвященной основам разработки надстроек, размещаемых в SharePoint. Для начала следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и предыдущими статьями из этой серии:
 

-  [Знакомство с созданием надстроек SharePoint с размещением в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 
-  [Развертывание и установка размещаемых в SharePoint надстроек SharePoint](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [Добавление настраиваемых столбцов в надстройки, размещенные в SharePoint](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in)
    
 
-  [Добавление настраиваемого типа контента в надстройки, размещенные в SharePoint](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in)
    
 
-  [Добавление веб-части на страницу в надстройке, размещенной в SharePoint](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [Добавление рабочего процесса к надстройке, размещенной в SharePoint](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in)
    
 

 **Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых в SharePoint, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с данной статьей. Кроме того, вы можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforePage.sln.
 

В этой статье описано, как добавить страницу справки в надстройку SharePoint "Employee Orientation" (Обучение сотрудников) и настроить ее на использование специальной таблицы стилей CSS. 
 

## <a name="add-a-page"></a>Добавление страницы


1. В **обозревателе решений** щелкните правой кнопкой мыши папку **Страницы** и выберите **Добавить** > **Новый элемент**. Откроется диалоговое окно **Добавление нового элемента** для узла **Office/SharePoint**.
    
 
2. Выберите элемент **Страница** и задайте для него имя nameHelp.aspx. 
    
 
3. Найдите в файле два элемента **asp:Content** и добавьте между ними приведенную ниже часть кода, заключенную в тег **asp:Content**.
    
```HTML
  <asp:Content ContentPlaceHolderID="PlaceHolderPageTitleInTitleArea" runat="server">
    Help
</asp:Content> 
```

4. Найдите элемент **asp:Content** с идентификатором **PlaceholderAdditionalPageHead** и добавьте к нему приведенную ниже часть кода.
    
```HTML
  <link rel="Stylesheet" type="text/css" href="../Content/App.css" />
```

5. Найдите элемент **asp:Content** с идентификатором **PlaceHolderMain** и удалите из него все дочерние элементы.
    
 
6. Добавьте к элементу **asp:Content** приведенное ниже содержимое.
    
```HTML
  <H3>Having a problem with the add-in?</H3>
<p> Call the help line for Fabrikam Add-ins:</p>
<p>1-555-555-5555</p>
```

7. Сохраните и закройте файл.
    
 
8. Откройте файл Default.aspx.
    
 
9. Найдите элемент **asp:Content** с идентификатором **PlaceHolderMain**, а затем добавьте в конце его содержимого приведенную ниже часть кода. 
    
```HTML
  <p><asp:HyperLink runat="server" NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Pages/Help.aspx';" 
    Text="Get help for the Employee Orientation add-in" /></p>

```

10. Сохраните и закройте файл.
    
 

## <a name="add-a-style-class-to-the-stylesheet"></a>Добавление класса стиля к таблице стилей


 

 

1. В **обозревателе решений** откройте файл app.css из папки **Содержимое** и добавьте в этот файл приведенную ниже строку.
    
```
  p {color: green;}
```

2. Сохраните и закройте файл.
    
 

## <a name="run-and-test-the-add-in"></a>Запуск и тестирование надстройки


 

 

1. Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Visual Studio выполнит временную установку надстройки на тестовом сайте SharePoint и сразу же запустит ее. 
    
 
2. Когда откроется страница надстройки по умолчанию, перейдите по ссылке **Get help for the Employee Orientation add-in** (Вызов справки для надстройки, посвященной обучению сотрудников), чтобы открыть страницу **Help** (Справка).
    
    Откроется настраиваемая страница. Две строки, заключенные в <p> теги, выделяются зеленым цветом.
    

    **Страница справки**

 

  ![Страница SharePoint с заголовком "Help" (Справка). Она содержит черную строку заголовка, за которой следуют две зеленые текстовые строки.](../../images/2df51ab0-5b24-4a37-8b6a-6e95dbb1aeaa.PNG)
 

    
    
 
3. Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.
    
 
4. Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуем отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.
    
 

## 
<a name="Nextsteps"> </a>

В следующей статье этой серии, [Добавление пользовательского кода клиентской обработки к надстройке SharePoint, размещенной в SharePoint](add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in), рассматривается добавление пользовательского кода клиентской обработки для столбца списка в надстройке SharePoint.
 

 

