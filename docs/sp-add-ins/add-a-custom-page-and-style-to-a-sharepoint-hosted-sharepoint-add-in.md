---
title: "Добавление пользовательских страницы и стиля в надстройку SharePoint, размещаемую в SharePoint"
description: "Добавьте пользовательскую страницу, добавьте класс стиля в таблицу стилей, а затем запустите и протестируйте надстройку."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: ff0376366f4dd003bdc84935841470e00c270696
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in"></a>Добавление собственной страницы и стиля в надстройку с размещением в SharePoint

Это седьмая часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых в SharePoint. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins.md) и предыдущими статьями этой серии, представленными в разделе [Знакомство с созданием надстроек SharePoint, размещаемых в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md#Nextsteps). 
    
> [!NOTE]
> Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых в SharePoint, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с этой статьей. Кроме того, вы можете скачать репозиторий на веб-странице [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforePage.sln.

Работая с этой статьей, вы добавите страницу справки в надстройку SharePoint "Employee Orientation" (Обучение сотрудников) и настроите ее так, чтобы в ней использовалась специальная таблица стилей CSS. 

## <a name="add-a-page"></a>Добавление страницы

1. В **обозревателе решений** щелкните правой кнопкой мыши папку **Pages** (Страницы) и выберите пункты **Добавить** > **Новый элемент**. Откроется диалоговое окно **Добавление нового элемента** для узла **Office/SharePoint**.

2. Выберите **Page** (Страница) и задайте имя **Help.aspx**. 

3. Найдите в файле два элемента **asp:Content** и добавьте между ними указанную ниже часть кода **asp:Content**.
    
    ```HTML
      <asp:Content ContentPlaceHolderID="PlaceHolderPageTitleInTitleArea" runat="server">
        Help
      </asp:Content> 
    ```

4. Найдите элемент **asp:Content** с идентификатором **PlaceholderAdditionalPageHead** и добавьте к нему указанную ниже часть кода.
    
    ```HTML
      <link rel="Stylesheet" type="text/css" href="../Content/App.css" />
    ```

5. Найдите элемент **asp:Content** с идентификатором **PlaceHolderMain** и удалите из него все дочерние элементы.

6. Добавьте указанное ниже содержимое в тот же элемент **asp:Content**.
    
    ```HTML
      <H3>Having a problem with the add-in?</H3>
      <p>Call the help line for Fabrikam Add-ins:</p>
      <p>1-555-555-5555</p>
    ```

7. Сохраните и закройте файл.

8. Откройте файл Default.aspx.

9. Найдите элемент **asp:Content** с идентификатором **PlaceHolderMain**, а затем добавьте указанную ниже часть кода в конец элемента. 
    
    ```HTML
      <p><asp:HyperLink runat="server" NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Pages/Help.aspx';" 
        Text="Get help for the Employee Orientation add-in" /></p>
    ```

10. Сохраните и закройте файл.

## <a name="add-a-style-class-to-the-stylesheet"></a>Добавление класса стиля в таблицу стилей

1. В **обозревателе решений** откройте файл app.css в папке **Contents** (Содержимое) и добавьте в этот файл указанную ниже строку.
    
    ```
      p {color: green;}
    ```

2. Сохраните и закройте файл.

## <a name="run-and-test-the-add-in"></a>Запуск и тестирование надстройки

1. Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Visual Studio выполнит временную установку надстройки на тестовом сайте SharePoint и сразу же запустит ее. 

2. Когда откроется страница надстройки, используемая по умолчанию, перейдите по ссылке **Get help for the Employee Orientation add-in** (Получить справку для надстройки Employee Orientation). Откроется страница **Help** (Справка).
    
   Откроется ваша пользовательская страница, и две строки, которые вы поместили между тегами `<p>`, будут иметь зеленый цвет.

   *Рис. 1. Страница "Help" (Справка)*

   ![Страница SharePoint с заголовком "Help" (Справка). Она содержит черную строку заголовка, за которой следуют две зеленые текстовые строки.](../images/2df51ab0-5b24-4a37-8b6a-6e95dbb1aeaa.PNG)

3. Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать последнюю.

4. Вы будете работать с этой надстройкой и решением Visual Studio при изучении других статей, поэтому при перерывах в работе рекомендуется отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.

## <a name="next-steps"></a>Дальнейшие действия
<a name="Nextsteps"> </a>

В следующей статье этой серии показано [добавление пользовательской клиентской обработки в надстройку SharePoint, размещаемую в SharePoint](add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in.md).
 

 

