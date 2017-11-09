---
title: "Создание рабочего процесса с помощью SharePoint Designer 2013 и платформы SharePoint Workflow"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c05e0127-c6f5-48b8-b8f2-cbcc30149c8b
ms.openlocfilehash: 06d6a0c8b59772bddad4dadd21b3b544868c42f2
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="creating-a-workflow-by-using-sharepoint-designer-2013-and-the-sharepoint-workflow-platform"></a>Создание рабочего процесса с помощью SharePoint Designer 2013 и платформы SharePoint Workflow
Узнайте, как установить, открыть и создать рабочий процесс с помощью SharePoint Designer 2013 и платформы SharePoint Workflow. 
   

## <a name="install-sharepoint-designer-2013"></a>Установка SharePoint Designer 2013
<a name="section1"> </a>

SharePoint Designer 2013 можно скачать бесплатно. Чтобы скачать и установить SharePoint Designer 2013, выполните описанные ниже шаги. 
  
    
    

### <a name="to-install-sharepoint-designer-2013"></a>Чтобы установить SharePoint Designer 2013:


1. Откройте свой веб-браузер и перейдите в Центр загрузки Майкрософт:  [http://www.microsoft.com/download](http://www.microsoft.com/download.aspx). 
    
  
2. Введите в поле поиска SharePoint Designer 2013.
    
  
3. Щелкните ссылку "SharePoint Designer 2013". 
    
  
4. Ознакомьтесь с обзором, системными требованиями и инструкциями по установке. Убедитесь, что ваша система совместима. 
    
  
5. Выберите 64-разрядный ( **x64**) или 32-разрядный ( **x86**) тип платформы, как показано на рисунке. 
    
  
6. Следуйте инструкции по установке SharePoint Designer 2013.
    
  

**Рисунок. Страница загрузки SharePoint Designer 2013**

  
    
    

  
    
    
![Страница загрузки SharePoint Designer 2013.](../images/SPD15-install-connect-1.png)
  
    
    

  
    
    

  
    
    

## <a name="open-sharepoint-designer-2013-and-connect-to-a-sharepoint-site"></a>Открытие SharePoint Designer 2013 и подключение к сайту SharePoint
<a name="section2"> </a>

SharePoint Designer 2013 устанавливается как приложение Office 2013. Чтобы открыть SharePoint Designer 2013 и подключиться к сайту SharePoint, выполните описанные ниже шаги. 
  
    
    

### <a name="to-open-sharepoint-designer-2013-and-connect-to-a-sharepoint-site"></a>Чтобы открыть SharePoint Designer 2013 и подключиться к сайту SharePoint:


1. Откройте SharePoint Designer 2013, выбрав его в меню **Пуск**. Нажмите значок **Пуск**, выберите пункт **Все программы**, а затем  **Microsoft Office 2013** и **SharePoint Designer 2013**. 
    
  
2. Щелкните **Открыть сайт** на начальной странице SharePoint Designer 2013.
    
  
3. Введите сайт SharePoint, к которому хотите подключиться. Например, http://www.contoso.com/sites/a-sharepoint-site.
    
  
4. Нажмите кнопку **Открыть**, чтобы открыть веб-сайт.
    
  
5. При необходимости введите свои учетные данные. (Если с компьютером, с которого вы выполнили вход, не интегрирована система безопасности, далее вам будет предложено ввести учетные данные.) Убедитесь, что вы используете учетные данные с правами доступа на сайт SharePoint.
    
  

## <a name="create-a-list-workflow-based-on-the-sharepoint-workflow-platform"></a>Создание рабочего процесса списка на основе платформы SharePoint Workflow
<a name="section3"> </a>

SharePoint Designer 2013 можно использовать для многих важных задач. Панель навигации используется для переключения между различными аспектами SharePoint Designer 2013. Чтобы создать новый рабочий процесс списка на основе платформы SharePoint Workflow, выполните описанные ниже шаги.
  
    
    

### <a name="to-create-a-workflow-based-on-the-sharepoint-workflow-platform"></a>Чтобы создать рабочий процесс на основе платформы SharePoint Workflow:


1. Щелкните на панели навигации узел "Рабочие процессы".
    
  
2. Щелкните выпадающее меню **Рабочий процесс списка** в разделе **Создание** ленты, как показано на рисунке.
    
  
3. Выберите список, который нужно связать с новым рабочим процессом.
    
  
4. В диалоговом окне **Создание рабочего процесса списка** введите название и описание рабочего процесса, а затем убедитесь, что **Тип платформы** установлен в **SharePoint Workflow**, как показано на рисунке.
    
    > **Примечание.** Если тип платформы "Рабочий процесс SharePoint" недоступен, то Workflow Manager не настроен для работы с фермой SharePoint. 
5. Нажмите кнопку **ОК**, чтобы создать рабочий процесс.
    
  

**Рисунок. Кнопка на ленте для создания нового рабочего процесса списка**

  
    
    

  
    
    
![SharePoint Designer 2013 — рабочий процесс "Создание списка"](../images/SPD15-install-connect-2.png)
  
    
    

  
    
    

  
    
    

**Рисунок. Диалоговое окно "Создание рабочего процесса списка"**

  
    
    

  
    
    
![Диалоговое окно создания рабочего процесса](../images/SPD15-install-connect-3.png)
  
    
    

  
    
    

  
    
    
Теперь, когда рабочий процесс создан, вы можете добавлять к нему нужные действия, условия, стадии, шаги и циклы. Эти компоненты доступны на ленте SharePoint Designer 2013, как показано на рисунке. 
  
    
    

**Рисунок. Элементы рабочего процесса для платформы SharePoint Workflow**

  
    
    

  
    
    
![Элементы рабочего процесса на ленте.](../images/SPD15-install-connect-4.png)
  
    
    

    
> **Примечание.** Вышеописанная процедура используется для создания рабочего процесса списка. Рабочие процессы для повторного использования и сайтов можно создавать с применением одной и той же процедуры с описанным ниже изменением. Вместо кнопки "Рабочий процесс списка" на ленте нажмите при создании рабочего процесса кнопку **Рабочий процесс для повторного использования** или **Рабочий процесс сайта**.
  
    
    

Дополнительные сведения о доступных компонентах для разработки рабочих процессов см. в статье [Краткий справочник по действиям рабочих процессов (платформа рабочих процессов SharePoint)](workflow-actions-quick-reference-sharepoint-workflow-platform.md).
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Новые возможности рабочих процессов SharePoint](http://msdn.microsoft.com/library/6ab8a28b-fa2f-4530-8b55-a7f663bf15ea.aspx)
    
  
-  [Начало работы с рабочими процессами SharePoint](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)
    
  
-  [Разработка рабочих процессов в SharePoint Designer и Visio](workflow-development-in-sharepoint-designer-and-visio.md)
    
  

  
    
    

