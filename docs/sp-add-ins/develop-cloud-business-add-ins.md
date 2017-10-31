---
title: "Разработка облачных бизнес-надстроек"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 9fea6e5b8133cceabfbb280af38d26078bc8dab3
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="develop-cloud-business-add-ins"></a><span data-ttu-id="b64a9-102">Разработка облачных бизнес-надстроек</span><span class="sxs-lookup"><span data-stu-id="b64a9-102">Develop cloud business add-ins</span></span>
 <span data-ttu-id="b64a9-p101">Облачные бизнес-надстройки основаны на технологии Visual Studio LightSwitch. Некоторые из задач разработки таких надстроек применяются только для шаблона "Облачная бизнес-надстройка", но большинство из них совпадает с задачами для клиентских HTML-надстроек LightSwitch.</span><span class="sxs-lookup"><span data-stu-id="b64a9-p101">Cloud business add-ins are based on Visual Studio LightSwitch technologies. Some of the tasks for developing cloud business add-ins are unique to the Cloud Business Add-in template, but most are the same as for LightSwitch HTML Client add-ins.</span></span>
 

 <span data-ttu-id="b64a9-p102">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p102">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="cloud-business-add-in-developer-tasks"></a><span data-ttu-id="b64a9-108">Задачи разработчика облачной бизнес-надстройки</span><span class="sxs-lookup"><span data-stu-id="b64a9-108">Cloud Business Add-in developer tasks</span></span>


- <span data-ttu-id="b64a9-p103">Облачные бизнес-надстройки создаются с помощью шаблона "Облачная бизнес-надстройка" в Visual Studio. См. статью [Создание облачной бизнес-надстройки](create-a-cloud-business-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p103">Cloud business add-ins are created by using the Cloud Business Add-in template in Visual Studio. See  [Create a cloud business add-in](create-a-cloud-business-add-in.md).</span></span>
    
 
- <span data-ttu-id="b64a9-p104">Используя библиотеки документов в SharePoint, можно создавать и загружать документы, связанные с определенными элементами списка или объекта. Дополнительные сведения см. в статье  [Сопоставление библиотеки документов с сущностью](associate-a-document-library-with-an-entity.md).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p104">By using the document library feature in SharePoint, you can create or upload documents associated with individual items in a list or entity. See  [Associate a document library with an entity](associate-a-document-library-with-an-entity.md).</span></span>
    
 
- <span data-ttu-id="b64a9-p105">В дополнение к шаблонам Office, доступным при добавлении документа в библиотеку документов SharePoint, вы можете использовать собственные шаблоны. Дополнительные сведения см. в статье  [Предоставление шаблона для библиотеки документов в облачной бизнес-надстройке](provide-a-template-for-a-document-library-in-a-cloud-business-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p105">In addition to the Office templates that are available when you add a document to a SharePoint document library, you can provide your own templates. See  [Provide a template for a document library in a cloud business add-in](provide-a-template-for-a-document-library-in-a-cloud-business-add-in.md).</span></span>
    
 
- <span data-ttu-id="b64a9-p106">Функции социальных медиа и совместной работы в SharePoint для Office 365 позволяют пользователям отслеживать действия со списком и добавлять комментарии. Вы легко можете создать канал новостей для облачной бизнес-надстройки, включив несколько свойств. Дополнительные сведения см. в статье  [Включение канала новостей для облачной бизнес-надстройки](enable-a-newsfeed-for-a-cloud-business-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p106">Social and collaboration features in SharePoint for Office 365 allow users to track activity on a list and add comments. You can easily create a newsfeed for your Cloud Business Add-in by enabling a couple of properties. See  [Enable a newsfeed for a cloud business add-in](enable-a-newsfeed-for-a-cloud-business-add-in.md).</span></span>
    
 

## <a name="html-client-developer-tasks"></a><span data-ttu-id="b64a9-118">Задачи разработчика HTML-клиента</span><span class="sxs-lookup"><span data-stu-id="b64a9-118">HTML Client developer tasks</span></span>


- <span data-ttu-id="b64a9-p107">При проектировании HTML-экранов в основном используются конструкторы и окна инструментов, но также можно использовать код для изменения этих экранов определенными способами. С помощью API-интерфейсов JavaScript для LightSwitch можно выполнить множество задач. Дополнительные сведения см. в  [практическом руководстве по изменению HTML-экрана с помощью кода](http://msdn.microsoft.com/en-us/library/jj733572.aspx).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p107">When you design HTML screens, you primarily use designers and tool windows, but you can also use code to modify those screens in specific ways. By using LightSwitch JavaScript APIs, you can perform many tasks. See  [How to: Modify an HTML Screen by Using Code](http://msdn.microsoft.com/en-us/library/jj733572.aspx).</span></span>
    
 
- <span data-ttu-id="b64a9-p108">При разработке надстройки, представляющей собой HTML-клиент, вы можете создавать экраны нескольких типов. См. статью [Выбор типа экрана для HTML-клиента приложения LightSwitch](http://msdn.microsoft.com/en-us/library/jj713590.aspx).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p108">When you develop an HTML client add-in, you can create several types of screens. See  [Choosing a Screen Type for an HTML Client](http://msdn.microsoft.com/en-us/library/jj713590.aspx).</span></span>
    
 
- <span data-ttu-id="b64a9-p109">Создайте экран для отображения или сбора информации на мобильном устройстве. См. статью [Практическое руководство. Создание экрана HTML-клиента](http://msdn.microsoft.com/en-us/library/jj713589.aspx).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p109">Create a screen to display or collect information on a mobile device. See  [How to: Create an HTML Client Screen](http://msdn.microsoft.com/en-us/library/jj713589.aspx).</span></span>
    
 
- <span data-ttu-id="b64a9-p110">Если создать диалоговое или всплывающее окно для надстройки, пользователи смогут отображать или задавать определенные сведения на телефоне, планшете или другом мобильном устройстве с клиентом этой надстройки. См.  [руководство по созданию диалогового или всплывающего окна](http://msdn.microsoft.com/en-us/library/jj713587.aspx).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p110">If you create a dialog or a popup for your add-in, users can display or specify information on a phone, tablet, or other mobile device that's running a client for that add-in. See  [How to: Create a Dialog or Popup](http://msdn.microsoft.com/en-us/library/jj713587.aspx).</span></span>
    
 
- <span data-ttu-id="b64a9-p111">С помощью конструктора экранов можно изменять внешний вид экранов в HTML-клиентов. Дополнительные сведения см. в  [руководстве по проектированию HTML-экрана с помощью конструктора экранов](http://msdn.microsoft.com/en-us/library/jj733575.aspx).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p111">By using the screen designer, you can modify the appearance of screens in an HTML client. See  [How to: Design an HTML Screen by Using the Screen Designer](http://msdn.microsoft.com/en-us/library/jj733575.aspx).</span></span>
    
 
- <span data-ttu-id="b64a9-p112">При разработке мобильной клиентской HTML-надстройки можно добавить код, который выполняется, когда пользователь нажимает кнопку на экране в этом клиенте. См.  [руководство по добавлению кнопки](http://msdn.microsoft.com/en-us/library/jj733573.aspx).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p112">When you develop an HTML mobile client add-in, you can add code that runs when the user taps a button on a screen in that client. See  [How to: Add a Button](http://msdn.microsoft.com/en-us/library/jj733573.aspx).</span></span>
    
 
- <span data-ttu-id="b64a9-p113">Вы можете получить введенное значение или показать вычисленное значение, добавив поле локального свойства на экран. См.  [руководство по добавлению локального свойства на экран](http://msdn.microsoft.com/en-us/library/jj733571.aspx).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p113">You can collect an input value or display a calculated value by adding a local property field to a screen. See  [How to: Add a Local Property to a Screen](http://msdn.microsoft.com/en-us/library/jj733571.aspx).</span></span>
    
 
- <span data-ttu-id="b64a9-p114">На экран можно добавить пользовательские элементы управления HTML. Они позволяют показывать или собирать сведения с большими возможностями, чем встроенные элементы управления HTML. Дополнительные сведения см. в  [руководстве по добавлению настраиваемого элемента управления на экран HTML](http://msdn.microsoft.com/en-us/library/jj733569.aspx).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p114">You can add custom HTML controls to a screen. By using custom controls, you can display or collect information in ways that exceed the capabilities of the built-in HTML controls. See  [How to: Add a Custom Control to an HTML Screen](http://msdn.microsoft.com/en-us/library/jj733569.aspx).</span></span>
    
 
- <span data-ttu-id="b64a9-p115">Фильтруя данные, отображаемые в HTML-клиенте, можно помочь пользователям определить самые актуальные данные для выполнения их задач. См.  [руководство по фильтрации данных в HTML-клиенте](http://msdn.microsoft.com/en-us/library/jj733574.aspx).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p115">By filtering the data that appears in your HTML client, you can help users identify the most relevant data for their tasks. See  [How to: Filter Data in an HTML Client](http://msdn.microsoft.com/en-us/library/jj733574.aspx).</span></span>
    
 
- <span data-ttu-id="b64a9-p116">При проектировании клиентской HTML-надстройки вы определяете, как пользователи открывают один экран на другом. Они могут открыть экран, выбрав элемент списка на другом экране или нажав кнопку в панели команд. См.  [руководство по управлению навигацией между HTML-экранами](http://msdn.microsoft.com/en-us/library/jj733570.aspx).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p116">As you design an HTML client add-in, you specify how users open one screen from another. They can open a screen by tapping either a list item on another screen or a button on the command bar. See  [How to: Control Navigation between HTML Screens](http://msdn.microsoft.com/en-us/library/jj733570.aspx).</span></span>
    
 
- <span data-ttu-id="b64a9-p117">В дополнение к стандартной навигации можно добавить меню навигации, позволяющее пользователям переходить непосредственно на другой экран. См.  [руководство по созданию меню навигации](http://msdn.microsoft.com/en-us/library/dn546744.aspx).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p117">In addition to the standard navigation, you can provide a navigation menu that allows users to jump directly to another screen. See  [How to: Create a Navigation Menu](http://msdn.microsoft.com/en-us/library/dn546744.aspx).</span></span>
    
 
- <span data-ttu-id="b64a9-p118">При разработке мобильной клиентской HTML-надстройки можно написать код JavaScript, который выполняется, когда пользователь инициирует определенное событие. Дополнительные сведения см. в  [руководстве по обработке событий экранов в мобильном клиенте](http://msdn.microsoft.com/en-us/library/jj863131.aspx).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p118">As you develop an HTML mobile client add-in, you can write JavaScript code that runs when a user initiates a certain event. See  [How to: Handle Screen Events in a Mobile Client](http://msdn.microsoft.com/en-us/library/jj863131.aspx).</span></span>
    
 
- <span data-ttu-id="b64a9-p119">Вы можете создавать мобильные надстройки, получающие и обновляющие рабочие процессы SharePoint, что помогает гарантировать выполнение бизнес-процессов в определенной последовательности. Например, рабочий процесс можно использовать для утверждения или обработки зарплатой ведомости. См.  [пошаговое руководство по доступу к рабочему процессу SharePoint](http://msdn.microsoft.com/en-us/library/dn282437.aspx).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p119">You can create mobile add-ins that access and update SharePoint workflows, which help ensure that business processes are performed in a particular sequence. For example, you might use a workflow to route a document for approval or to process a payroll. See  [Walkthrough: Accessing a SharePoint Workflow](http://msdn.microsoft.com/en-us/library/dn282437.aspx).</span></span>
    
 
- <span data-ttu-id="b64a9-p120">С помощью LightSwitch можно создать HTML-клиент, в котором мобильные пользователи могут просматривать, добавлять и обновлять данные из удаленных расположений с использованием современных сенсорных устройств, таких как смартфоны и планшеты. В этом пошаговом руководстве создается клиент для вымышленной грузовой компании, Contoso Moving, который поможет сотрудникам оценивать требуемое количество людей, грузовиков и коробок. См.  [пошаговое руководство по созданию клиента для мобильных пользователей](http://msdn.microsoft.com/en-us/library/jj674624.aspx).</span><span class="sxs-lookup"><span data-stu-id="b64a9-p120">By using LightSwitch, you can create an HTML client in which mobile users can view, add, and update data from remote locations by using modern, touch-oriented devices such as phones and tablets. In this walkthrough, you'll create a client for a fictional moving company, Contoso Moving, so that its customer-service staff can more easily estimate how many people, trucks, and boxes each job will require. See  [Walkthrough: Creating a Client for Mobile Users](http://msdn.microsoft.com/en-us/library/jj674624.aspx).</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="b64a9-152">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b64a9-152">Additional resources</span></span>
<span data-ttu-id="b64a9-153"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b64a9-153"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="b64a9-154">Создание облачных бизнес-надстроек</span><span class="sxs-lookup"><span data-stu-id="b64a9-154">Create cloud business add-ins</span></span>](create-cloud-business-add-ins.md)
    
 
-  [<span data-ttu-id="b64a9-155">Экраны HTML-клиента для приложений LightSwitch</span><span class="sxs-lookup"><span data-stu-id="b64a9-155">HTML Client Screens for LightSwitch Add-ins</span></span>](http://msdn.microsoft.com/en-us/library/jj674623.aspx)
    
 

