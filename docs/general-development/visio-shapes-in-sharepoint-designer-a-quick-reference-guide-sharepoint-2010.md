---
title: "Фигур Visio в SharePoint Designer 2013 краткий справочник (платформа рабочих процессов SharePoint 2010)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 51bc37fd-37de-4ad0-a75a-bdf7333bc80c
ms.openlocfilehash: d685265148d2e626982a6010f5f48a00d366863f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="visio-shapes-in-sharepoint-designer-2013-a-quick-reference-guide-sharepoint-2010-workflow-platform"></a>Фигур Visio в SharePoint Designer 2013: краткий справочник (платформа рабочих процессов SharePoint 2010)
Можно создать рабочий процесс в Microsoft Visio профессиональный 2013 и экспортировать его в Microsoft SharePoint Designer 2013. В этом руководстве идентифицирует фигур Visio, используемые для создания рабочего процесса.Используйте эту статью ссылку только в том случае, если пользователь работает в SharePoint Designer 2013, но продолжить использование платформы рабочих процессов SharePoint 2010.Фигуры для платформы рабочих процессов SharePoint 2010 поступают в трех наборы элементов: **действия - рабочего процесса SharePoint 2010**, **условия - рабочего процесса SharePoint 2010** и **конца - рабочего процесса SharePoint 2010**.
## <a name="workflow-actions"></a>Действия рабочего процесса
<a name="section1"> </a>

Действия рабочего процесса, определенных операций выполняет этого рабочего процесса. Каждый рабочий процесс должен содержать по крайней мере одно действие.
  
    
    
Действия в этом списке организованы в категории на основании их области приложения в рабочем процессе. Например действия, которые влияют на поведение элемента списка собраны в разделе **Действия со списком** и действия, связанные с наборы документов собраны в разделе **Настройка действия с документами**. Категории для действий являются:
  
    
    

-  [Основные действия](visio-shapes-in-sharepoint-designer-a-quick-reference-guide-sharepoint-2010.md#section1a) Это наиболее часто используемые действия в рабочий процесс.
    
  
-  [Действия с наборами документов](visio-shapes-in-sharepoint-designer-a-quick-reference-guide-sharepoint-2010.md#section1e) Как правило в рабочих процессов, связанных с библиотекой документов или типа контента документа используются следующие действия.
    
  
-  [Действия со списками](visio-shapes-in-sharepoint-designer-a-quick-reference-guide-sharepoint-2010.md#section1b) Операции для элементов списка выполнить следующие действия.
    
  
-  [Действия с отношениями](visio-shapes-in-sharepoint-designer-a-quick-reference-guide-sharepoint-2010.md#section1d) Одно действие в этой категории ищет руководителя пользователя и сохраняет их в переменной.
    
  
-  [Действия с задачами](visio-shapes-in-sharepoint-designer-a-quick-reference-guide-sharepoint-2010.md#section1c) Эти действия связаны с формы операций, свои отзывы и предложения и утверждения.
    
  

> **Важные:** Большая часть фигуры действия, которые можно вставить в рабочий процесс SharePoint в Visio требуется дополнительная настройка при импорте рабочего процесса в SharePoint Designer. В Visio не забудьте использовать функцию комментариев для каждой фигуры действие для указания параметров или конфигурации действия. 
  
    
    


### <a name="core-actions"></a>Основные действия
<a name="section1a"> </a>

Эти действия наиболее часто используемые и могут использоваться в любой тип рабочего процесса или шаг.



|**Действие фигуры Visio**|**Соответствующее действие в SharePoint Designer**|**Описание**|
|:-----|:-----|:-----|
|![Добавление комментария](../images/spd15-addcomment-visio.JPG)|Это действие Visio  это то же, что действие **Добавить комментарий** в SharePoint Designer 2013 и отображается как: <br/> ![Добавление комментария](../images/spd15-addcomment-txt.JPG)  <br/>  **Примечание:** Комментарии остаются видимыми, когда рабочий процесс экспортируется в Visio.           |**Добавление комментария** <br/> Используйте это действие для оставлять комментарии информативных данных в конструкторе рабочих процессов для справочных целей. Это особенно удобно в тех случаях, когда других пользователей, совместное редактирование рабочего процесса. Например если переменная в текущем рабочего процесса не имеет понятное имя, используйте это действие для добавления комментария, чтобы указать, что означает эта переменная в рабочем процессе.<br/> |
|![Добавление времени к дате](../images/spd15-addtimetodate-visio.JPG)|Это действие Visio же, как **Добавить время к дате** действие в SharePoint Designer 2013 и отображается как: <br/> ![Добавление времени к дате](../images/spd15-addtimetodate-txt.JPG)|**Добавление времени к дате** <br/> Используйте это действие для добавления определенное время в минутах, часов, дней, месяцев или лет к дате и сохранить значение выходные данные в качестве переменной. Дата может быть текущую дату, определенную дату или подстановки.<br/> |
|![Выполнение расчета](../images/spd15-docalc-visio.JPG)|Это действие Visio  это то же, что действие **Выполните вычислений** в SharePoint Designer 2013 и отображается как: <br/> ![Выполнение расчета](../images/spd15-docalc-txt.JPG)|**Выполнение расчета** <br/> Используйте это действие для выполнения вычислений, таких как добавление, вычитания, умножения и деления двух значений и выходных данных значение сохраняется в переменной.  <br/> |
|![Запись в журнал](../images/spd15-LogHist-visio.JPG)|Это действие Visio  это то же, что действие **журнала в журнал** в SharePoint Designer 2013 и отображается как: <br/> ![Запись в журнал](../images/spd15-LogHist-txt.JPG)|**Запись в журнал** <br/> Это действие используется для записи в журнал сообщение о рабочем процессе в свой список журнала. Сообщение может быть Сводка событий рабочего процесса или что-либо значительные о рабочем процессе. Списке журнала рабочего процесса могут быть полезны для устранения проблем с рабочим процессом.<br/> |
|![Приостановка в течение определенного периода](../images/spd15-PauseDuration-visio.JPG)|Это действие Visio совпадает с **паузу в течение** действие в SharePoint Designer 2013 и отображается как: <br/> ![Приостановка в течение определенного периода](../images/spd15-PauseDuration-txt.JPG)|**Приостановка в течение определенного периода** <br/> Используйте это действие для приостановки рабочего процесса в течение определенного периода времени в несколько дней, часов и минут.  <br/> **Примечание:** Задержка — это влияют интервал задания таймера, который имеет значение по умолчанию 5 минут.           |
|![Приостановка до даты](../images/spd15-PauseDate-visio.JPG)|Это действие Visio  это то же, что действие **Паузу до даты** в SharePoint Designer 2013 и отображается как: <br/> ![Приостановка до даты](../images/spd15-PauseDate-txt.JPG)|**Приостановка до даты** <br/> Используйте это действие для приостановить рабочий процесс до определенной даты. Можно добавить текущую дату, определенную дату или подстановки.<br/> |
|![Установка времени для поля даты и времени](../images/spd15-SetTimePortion-visio.JPG)|Это действие Visio  это то же, что действие **Задать часть из времени поля даты и времени** в SharePoint Designer 2013 и отображается как: <br/> ![Установка времени для поля даты и времени](../images/spd15-SetTimePortion-txt.JPG)|**Задать время для поля даты и времени** <br/> Используйте это действие для создания временной метки и значение выходных данных хранилища в переменной. Можно задания времени в часы, минуты и добавить текущую дату, определенную дату или подстановки.<br/> |
|![Установка состояния рабочего процесса](../images/spd15-SetWFStatus-visio.JPG)| Это действие Visio  это то же, что действие **Задать состояние рабочего процесса** в SharePoint Designer 2013 и отображается как: <br/> ![Установка состояния рабочего процесса](../images/spd15-SetWFStatus-txt.JPG)Невозможно переименование или удаление значение состояния после его создания. Тем не менее нет необходимости использовать его. <br/>  Пользовательское состояние применимо только к текущему рабочему процессу, и его невозможно использовать в другом рабочем процессе. <br/>  Рабочий процесс не может использовать пользовательские значения состояния, которые определены в действии, если действие используется в шаге олицетворения. <br/> |**Установка состояния рабочего процесса** <br/> Используйте это действие для задания состояния рабочего процесса. Значения по умолчанию  **отменено**, **Утверждено** и **Отклонено**. <br/> Можно ввести новое значение состояние в раскрывающемся списке в действии. После ввода значение состояния запись автоматически добавляется в раскрывающемся списке.<br/> Если действие **Задать состояние рабочего процесса** на последнем этапе рабочего процесса также применения пользовательское значение, видно ваше пользовательское значение в столбце **состояние** в списке при Приостановка рабочего процесса и уведомление. <br/> |
|![Установка переменной рабочего процесса](../images/spd15-SetWFVar-visio.JPG)|Это действие Visio  это то же, что действие **Задать переменную рабочего процесса** в SharePoint Designer 2013 и отображается как: <br/> ![Установка переменной рабочего процесса](../images/spd15-SetWFVar-txt.JPG)|**Установка переменной рабочего процесса** <br/> Используйте это действие для присвоено значение переменной рабочего процесса. Используйте это действие рабочего процесса, чтобы присвоить переменной данных.<br/> |
|![Остановка рабочего процесса](../images/spd15-StopWF-visio.JPG)|Это действие Visio  это то же, что действие **остановка рабочего процесса** в SharePoint Designer 2013 и отображается как: <br/> ![Остановка рабочего процесса](../images/spd15-StopWF-txt.JPG)|**Остановка рабочего процесса** <br/> Используйте это действие для остановки текущего экземпляра рабочего процесса и войдите сообщение в списке **Журнала рабочего процесса**. Сообщение, указанные в действие будет отображаться в столбце **Описание** в журнал рабочего процесса после завершения рабочего процесса. <br/> |
   

### <a name="list-actions"></a>Действия со списками
<a name="section1b"> </a>

Эти действия используются для элементов списка.
  
    
    



|**ДЕЙСТВИЕ ФИГУРЫ VISIO**|**СООТВЕТСТВУЮЩЕЕ ДЕЙСТВИЕ В SHAREPOINT DESIGNER**|**Описание**|
|:-----|:-----|:-----|
|![Добавление разрешений для элемента списка](../images/spd15-AddListItemPerms-visio.JPG)|Это действие Visio  это то же, что действие **Добавить разрешения для элемента списка** в SharePoint Designer 2013 и отображается как: <br/> ![Добавить разрешения для элемента](../images/spd15-AddListItemPerms-txt.JPG)    **Примечание:** это действие доступно только в пределах шаг олицетворения.           |**Добавление разрешений для элемента списка** <br/> Это действие предоставляет права отдельные уровни разрешений для элемента к определенным пользователям.  <br/> |
|![Возвращение элемента](../images/spd15-CheckInItem-visio.JPG)|Это действие Visio совпадает с действия **Проверки в элемента** в SharePoint Designer 2013 и отображается как: <br/> ![Возвращение элемента](../images/spd15-CheckInItem-txt.JPG)|**Возвращение элемента** <br/> Это действие проверяет в элементе, который выдается.  <br/> **Примечание:** Можно указать только в элементы из библиотеки документов.           |
|![Извлечение элемента](../images/spd15-CheckOutItem-visio.JPG)|Это действие Visio совпадает с действия **Проверьте масштабирование элемента** в SharePoint Designer 2013 и отображается как: <br/> ![Извлечение элемента](../images/spd15-CheckOutItem-txt.JPG)|**Извлечение элемента** <br/> Это действие используется для извлечения элемента. Рабочий процесс проверяет, если элемент в базу данных, перед его извлекает документ.<br/> **Примечание:** Можно указать только элементов из библиотеки на вашем сайте.           |
|![Копирование элемента списка](../images/spd15-CopyListItem-visio.JPG)|Это действие Visio  это то же, что действие **Копирование элемента списка** в SharePoint Designer 2013 и отображается как: <br/> ![Копирование элемента списка](../images/spd15-CopyListItem-txt.JPG)|**Копирование элемента списка** <br/> Это действие используется для копирования элемента списка в другой список. Если в элементе списка документа, рабочий процесс также копирует документ в целевом списке.<br/> **Важные:** Необходимо иметь хотя бы один столбец одинаковым в исходной и целевой списков.           |
|![Создание элемента списка](../images/spd15-CreateListItem-visio.JPG)|Это действие Visio  это то же, что действия **Создание элемента списка** в SharePoint Designer 2013 и отображается как: <br/> ![Создание элемента списка](../images/spd15-CreateListItem-txt.JPG)|**Создание элемента списка** <br/> Это действие используется для создания нового элемента списка в списке, который указан. Можно предоставить поля и значения в новый элемент.<br/> Это действие можно использовать всякий раз, когда новый элемент должен быть создана на конкретные сведения.  <br/> **Примечание:** Выходной переменной — это идентификатор элемента, созданные в списке.           |
|![Удаление элемента](../images/spd15-DeleteItem-visio.JPG)|Это действие Visio  это то же, что действие **Удалить элемент** в SharePoint Designer 2013 и отображается как: <br/> ![Удаление элемента](../images/spd15-DeleteItem-txt.JPG)|**Удаление элемента** <br/> Это действие используется для удаления элемента.  <br/> |
|![Отмена извлечения элемента](../images/spd15-DiscardItem-visio.JPG)|Это действие Visio  это то же, что действия **Отменить проверьте масштабирование элемента** в SharePoint Designer 2013 и отображается как: <br/> ![Отмена извлечения элемента](../images/spd15-DiscardItem-txt.JPG)|**Отмена извлечения элемента** <br/> Используйте это действие, если элемент извлечен, изменения были внесены в нее и отменить изменения и извлекать элемент обратно.  <br/> |
|![Наследование разрешений для элемента списка](../images/spd15-InheritListItemPerms-visio.JPG)|Это действие Visio  это то же, что действие **Наследовать разрешения родительского элемента списка** в SharePoint Designer 2013 и отображается как: <br/> ![Наследование разрешений для элемента списка](../images/spd15-InheritListItemPerms-txt.JPG)    **Примечание:** это действие доступно только в шаг олицетворения.           |**Наследование разрешений для элемента списка** <br/> Если элемент имеет уникальные разрешения, это действие можно использовать для отображения элемента наследовать разрешения родительского из списка.  <br/> |
|![Удаление разрешений для элемента списка](../images/spd15-RmListItemPerms-visio.JPG)|Это действие Visio  это то же, что действие s **Удалить разрешения элемента списка** в SharePoint Designer 2013 и отображается как:  <br/> ![Удаление разрешений для элемента списка](../images/spd15-RmListItemPerms-txt.JPG)    **Примечание:** это действие доступно только в шаг олицетворения.           |**Удаление разрешений для элемента списка** <br/> Это действие удаляет разрешения из элемента для определенных пользователей.  <br/> |
|![Замена разрешений для элемента списка](../images/spd15-ReplaceListItemPerms-visio.JPG)|Это действие Visio  это то же, что действие **Заменить разрешения для элемента списка** в SharePoint Designer 2013 и отображается как: <br/> ![Заменить разрешения для элемента списка](../images/spd15-ReplaceListItemPerms-txt.JPG)    **Примечание:** это действие доступно только в шаг олицетворения.           |**Замена разрешений для элемента списка** <br/> Разрешения для текущего элемента заменяет новые разрешения, заданные в действие.  <br/> |
|![Установка состояния утверждения контента](../images/spd15-SetContentApprovalStatus-visio.JPG)|Это действие Visio  это то же, что действие **Задать состояние утверждения контента** в SharePoint Designer 2013 и отображается как: <br/> ![Задать состояние утверждения контента](../images/spd15-SetContentApprovalStatus-txt.JPG)    **Примечание:** утверждения контента должно быть включено в список для этого действия.|**Установка состояния утверждения контента** <br/> При наличии утверждение контента включен в списке использовать это действие присвоено значение, например, Утверждено, то поле состояние утверждения контента отклонено, или ожидающие. Особое состояние можно ввести в действие.<br/> **Примечание:** Действие **Задать состояние утверждения контента** работы на текущий элемент, который выполняется рабочий процесс, поэтому действие недоступен в рабочий процесс сайта.          |
|![Установка поля в текущем элементе](../images/spd15-SetFieldCurrItem-visio.JPG)|Это действие Visio  это то же, что действие **Задать поле в текущем элементе** в SharePoint Designer 2013 и отображается как: <br/> ![Установка поля в текущем элементе](../images/spd15-SetFieldCurrItem-txt.JPG)|**Установка поля в текущем элементе** <br/> Используйте действие, чтобы задать поле в текущем элементе значение.  <br/> **Примечание:** Если вы хотите приостановить рабочий процесс, пока не изменяется значение поля, используйте действие **ждать изменения поля в текущем элементе** .          Действие **Задать поле в текущем элементе** не должны использоваться в рабочий процесс сайта. <br/> |
|![Обновление элемента списка](../images/spd15-UpdateListItem-visio.JPG)|Это действие Visio  это то же, что действие **Обновление элемента списка** в SharePoint Designer 2013 и отображается как: <br/> ![Обновление элемента списка](../images/spd15-UpdateListItem-txt.JPG)|**Обновление элемента списка** <br/> Используйте это действие для обновления элемента списка. В этих полях можно указать поля и новые значения.<br/> |
|![Ожидание изменения поля в текущем элементе](../images/spd15-Wait4FieldChange-visio.JPG)|Это действие Visio  это то же, что действие **ждать изменения поля в текущем элементе** в SharePoint Designer 2013 и отображается как: <br/> ![Ожидание изменения поля](../images/spd15-Wait4FieldChange-txt.JPG)|**Ожидание изменения поля в текущем элементе** <br/> Это действие приостанавливает рабочий процесс, пока поле в текущем элементе изменился на новое значение.  <br/> **Примечание:** Если вы хотите рабочего процесса, чтобы изменить значение поля, а не имеют ожидать в поле, чтобы изменить рабочий процесс, используйте действие **Задать поле в текущем элементе** .          |
   

### <a name="task-actions"></a>Действия с задачами
<a name="section1c"> </a>

Действия в этой категории относятся к элементам задач. Эти действия применяются только к сайтам SharePoint под управлением SharePoint.
  
    
    




|**ДЕЙСТВИЕ ФИГУРЫ VISIO**|**СООТВЕТСТВУЮЩЕЕ ДЕЙСТВИЕ В SHAREPOINT DESIGNER**|**Описание**|
|:-----|:-----|:-----|
|![Назначение формы группе](../images/spd15-AssignForm2Grp-visio.JPG)|Это действие Visio  это то же, что действие **назначить форму группе** в SharePoint Designer 2013 и отображается как: <br/> ![Назначение формы группе](../images/spd15-AssignForm2Grp-txt.JPG)|**Назначение формы группе** <br/> Это действие используется для создания пользовательской формы задач с помощью настраиваемого поля.  <br/> Это действие можно использовать для назначения задачи одного или нескольких участников или группам, приглашений, для выполнения своих задач. Участники предоставляют их ответы ИТ поля настраиваемой задачи форм и завершении с задачей, нажмите кнопку **Завершить задачу** в форме.<br/> |
|![Назначение элемента списка дел](../images/spd15-AssignToDoItem-visio.JPG)|Это действие Visio  это то же, что действие **назначить задание** в SharePoint Designer 2013 и отображается как: <br/> ![Назначение элемента списка дел](../images/spd15-AssignToDoItem-txt.JPG)|**Назначение элемента списка дел** <br/> Это действие используется для назначения задачи для каждого из участников, должен выполнять свои задачи, а затем, когда они выполняются, нажмите кнопку **Завершить задачу** на их формы задачи. <br/> |
|![Сбор данных от пользователя](../images/spd15-CollectDataFrUser-visio.JPG)|Это действие Visio  это то же, что действие **Собирать данные от пользователя** в SharePoint Designer 2013 и отображается как: <br/> ![Сбор данных от пользователя](../images/spd15-CollectDataFrUser-txt.JPG)|**Сбор данных от пользователя** <br/> Это действие используется для назначения задачи участнику, должен предоставить необходимые сведения в форме пользовательских задач, а затем нажмите кнопку **Завершить задачу** в форме задачи. <br/> Это действие имеет предложение output. Это означает, что рабочий процесс хранит сведения, возвращаемые действие в соответствующей переменной. Идентификатор элемента списка элемента выполненной задачи из действия хранится в переменной собирать.  <br/> |
|![Установка процесса утверждения](../images/spd15-StartApprovalProc-visio.JPG)|Это действие Visio  это то же, что действие **Запуск процесса утверждения** в SharePoint Designer 2013 и отображается как: <br/> ![Запуск процесса утверждения для набора документов](../images/spd15-StartApprovalProc-txt.JPG)|**Установка процесса утверждения** <br/> Используйте это действие для маршрутизации документов на утверждение. Утверждающие могут утвердить или отклонить документ, переназначение задачи утверждения или запрос изменения.<br/> Можно назначать задачи для внутренних и внешних участников в действии. Внешний участник может быть сотрудник в вашей организации не будет пользователя в коллекции веб-сайтов или всем пользователям за пределами вашей организации.<br/> |
|![Запуск процесса сбора отзывов](../images/spd15-StartFeedback-visio.JPG)|Это действие Visio же, как **Начать процесс сбора отзывов** действие в SharePoint Designer 2013 и отображается как: <br/> ![Запуск процесса сбора отзывов](../images/spd15-StartFeedback-txt.JPG)|**Запуск процесса сбора отзывов** <br/> С помощью этого действия можно назначать элементы задачи для обратной связи для пользователей в определенном порядке код последовательный или параллельный. Значение по умолчанию — параллельный. Пользователи или исполнители задачи можно также переназначить другим пользователям. После завершения пользователей они нажмите кнопку **Отправьте свои отзывы и предложения** , чтобы указать завершение задачи. <br/> Можно назначать задачи для внутренних и внешних участников в действии. Внешний участник может быть сотрудник в вашей организации не будет пользователя в коллекции веб-сайтов или всем пользователям за пределами вашей организации.<br/> |
|![Запуск настраиваемого процесса задач](../images/spd15-StartCustomTask-visio.JPG)|Это действие Visio  это то же, что действие **Начать настраиваемый рабочий процесс** в SharePoint Designer 2013 и отображается как: <br/> ![Запуск настраиваемого процесса задач](../images/spd15-StartCustomTask-txt.JPG)|**Запуск настраиваемого процесса задач** <br/> **Начать настраиваемый рабочий процесс** действие  это шаблон процесса утверждения, которые можно использовать другие действия утверждения не соответствуют требованиям. <br/> |
   

### <a name="relational-actions"></a>Действия с отношениями
<a name="section1d"> </a>

Одно действие в этой категории ищет руководителя пользователя и сохраняет их в переменной. Это действие применяется только к сайтам SharePoint под управлением SharePoint.
  
    
    




|**ДЕЙСТВИЕ ФИГУРЫ VISIO**|**СООТВЕТСТВУЮЩЕЕ ДЕЙСТВИЕ В SHAREPOINT DESIGNER**|**Описание**|
|:-----|:-----|:-----|
|![Найти руководителя для пользователя](../images/spd15-LookupMgr4User-visio.JPG)|Это действие Visio  это то же, что действие **Найти руководителя для пользователя** в SharePoint Designer 2013 и отображается как: <br/> ![Найти руководителя для пользователя](../images/spd15-LookupMgr4User-txt.JPG)|**Найти руководителя для пользователя** <br/> Это действие используется для поиска руководителя пользователя. Значение вывода хранится в переменной.<br/> **Примечание:** Для этого действия для правильной работы службы профилей пользователей должен работать под управлением в SharePoint.           |
   

### <a name="document-set-actions"></a>Действия с наборами документов
<a name="section1e"> </a>

Некоторые действия рабочего процесса доступны только сопоставлен рабочий процесс для библиотеки документов, таких как Общие документы или типа контента документа.
  
    
    




|**ДЕЙСТВИЕ ФИГУРЫ VISIO**|**СООТВЕТСТВУЮЩЕЕ ДЕЙСТВИЕ В SHAREPOINT DESIGNER**|**Описание**|
|:-----|:-----|:-----|
|![Отправка утверждения для набора документов](../images/spd15-SendApproval4DocSet-visio.JPG)|Это действие Visio  это то же, что действие **Начать процесс утверждения задать документа** в SharePoint Designer 2013 и отображается как: <br/> ![Запуск процесса утверждения для набора документов](../images/spd15-SendApproval4DocSet-txt.JPG)|**Отправка утверждения для набора документов** <br/> Используйте это действие, чтобы начать процесс утверждения для набора документов.  <br/> |
|![Отправка набора документов в репозиторий](../images/spd15-SendDocSet2Repos-visio.JPG)|Это действие Visio  это то же, что действие **Отправить набор документов в репозиторий** в SharePoint Designer 2013 и отображается как: <br/> ![Отправка набора документов в репозиторий](../images/spd15-SendDocSet2Repos-txt.JPG)|**Отправка набора документов в репозиторий** <br/> Используйте это действие для перемещения или копирования набор документов в репозиторий документов. Репозиторий документов может быть библиотеки в сайт SharePoint или сайта на собственный как Центр документов, маршрутизации записей в определенное назначение на основе правил, которые можно определить.<br/> |
|![Отправка документа в репозиторий](../images/spd15-SendDoc2Repos-visio.JPG)|Это действие Visio  это то же, что действие **Отправить документ в репозиторий** в SharePoint Designer 2013 и отображается как: <br/> ![Отправка документа в репозиторий](../images/spd15-SendDoc2Repos-txt.JPG)|**Отправка документа в репозиторий** <br/> Используйте это действие для перемещения или копирования документа в репозитории документов. Репозиторий документов может быть библиотеки в сайт SharePoint или сайта на собственный как Центр документов, маршрутизации записей в определенное назначение на основе правил, которые можно определить.<br/> |
|![Установка состояния утверждения контента для набора документов](../images/spd15-SetContentApprStatus-visio.JPG)|Это действие Visio  это то же, что действие **Задать состояние утверждения контента для набора документов** в SharePoint Designer 2013 и отображается как: <br/> ![Установка состояния утверждения контента для набора документов](../images/spd15-SetContentApprStatus4DocSet-txt.JPG)|**Задать состояние утверждения контента для набора документов** <br/> Используйте это действие для задания утверждения контента документа, **Утверждено**, **Отклонено** или **ожидающие**.  <br/> |
   

## <a name="workflow-conditions"></a>Условия бизнес-процессов
<a name="section2"> </a>

Условие рабочего процесса  ветвления точка в рабочем процессе. Условие рабочего процесса сравнивает входные данные с заданным значением. Если они совпадают, рабочего процесса исходя из одного филиала; в противном случае следует других филиалов.
  
    
    

> **Важные:** Большая часть условие фигуры, которые можно вставить в рабочий процесс SharePoint в Visio требуется дополнительная настройка при импорте рабочего процесса в SharePoint Designer. В Visio не забудьте использовать функцию комментариев для каждой фигуры условие для указания критерии условия. 
  
    
    


### <a name="general-conditions"></a>Общие условия

В этом разделе описываются условия, которые доступны в SharePoint Designer 2013 для списков и рабочих процессов для повторного использования списков, независимо от того, которые списком или типом контента рабочий процесс связан с.
  
    
    




|**ФИГУРА УСЛОВИЯ VISIO**|**СООТВЕТСТВУЮЩИЙ УСЛОВИЕ В SHAREPOINT DESIGNER**|**ОПИСАНИЕ УСЛОВИЯ**|
|:-----|:-----|:-----|
|![Сравнение источника данных](../images/spd15-CompareDataSrc-visio.JPG)|Это условие Visio  это то же, что **Если любое значение равно указанному значению** условие в SharePoint Designer 2013 и отображается как: <br/> ![Значение равно значению](../images/spd15-CompareDataSrc-txt.JPG)|**Сравнение источника данных** <br/> Это условие сравниваются два значения. Можно указать, следует ли значения равно или не равно.<br/> |
|![Сравнение поля документа](../images/spd15-CompareDocField-visio.JPG)|Это условие Visio  это то же, что **Если текущее поле элемента равно указанному значению** условие в SharePoint Designer 2013 и отображается как: <br/> ![Если текущее поле элемента равно значению](../images/spd15-CompareDocField-txt.JPG)|**Сравнение поля документа** <br/> Это условие проверяет поле со значением, который указан. Можно указать, следует ли значения равно или не равно.<br/> |
|![Создано определенным человеком](../images/spd15-CreatedBySpecPerson-visio.JPG)|Это условие Visio  это то же, что **создано определенным человеком** условие в SharePoint Designer 2013 и отображается как: <br/> ![Если создано определенным человеком](../images/spd15-CreatedBySpecPerson-txt.JPG)|**Создано определенным человеком** <br/> Это условие проверяет, если элемент был создан конкретным пользователем. Пользователь может указан как адрес электронной почты, например olivier@contoso.com, или выборе от пользователей SharePoint, Exchange и Active Directory.<br/> **Примечание:** Адрес электронной почты и имя пользователя, с учетом регистра. Рекомендуется выбрать пользователя имя или адрес электронной почты для убедитесь, что используется правильный регистр. При вводе пользователем имя или адрес электронной почты, должен соответствовать регистру учетной записи. Например, если созданные contoso\\Алексей не будет оценивать значение true, если учетная запись пользователя является Contoso\\Алексей.           |
|![Создано в рамках определенного диапазона дат](../images/spd15-CreatedInSpecDateSpan-visio.JPG)|Это условие Visio совпадает с условие **охватывать создано в конкретный день** в SharePoint Designer 2013 и отображается как: <br/> ![Если создано в рамках определенного диапазона дат](../images/spd15-CreatedInSpecDateSpan-txt.JPG)|**Создан в конкретном диапазоне дат** <br/> Это условие проверяет, если был создан между заданными датами. Можно использовать текущую дату, определенную дату или подстановки.<br/> |
|![Изменено определенным человеком](../images/spd15-ModifiedBySpecPerson-visio.JPG)|Это условие Visio  это то же, что условие **изменен конкретным пользователем** в SharePoint Designer 2013 и отображается как: <br/> ![Если изменено определенным человеком](../images/spd15-ModifiedBySpecPerson-txt.JPG)|**Изменено определенным человеком** <br/> Это условие используется для проверки, если изменения элемента, указанного пользователем. Пользователь может указан как адрес электронной почты, например olivier@contoso.com, или выборе от пользователей SharePoint, Exchange и Active Directory.<br/> **Примечание:** Адрес электронной почты и имя пользователя, с учетом регистра. Рекомендуется выбрать пользователя имя или адрес электронной почты для убедитесь, что используется правильный регистр. При вводе пользователем имя или адрес электронной почты, должен соответствовать регистру учетной записи. Например, если изменено contoso\\Алексей не будет оценивать значение true, если учетная запись пользователя является Contoso\\Алексей.           |
|![Изменено в рамках определенного диапазона дат](../images/spd15-ModifiedInSpecDateSpan-visio.JPG)|Это условие Visio совпадает с условие **охватывать изменено в конкретный день** в SharePoint Designer 2013 и отображается как: <br/> ![Если изменено в рамках определенного диапазона дат](../images/spd15-ModifiedInSpecDateSpan-txt.JPG)|**Изменено в рамках определенного диапазона дат** <br/> Это условие проверяет, если изменения элемента между заданными датами. Можно использовать текущую дату, определенную дату или подстановки.<br/> |
|![Поле заголовка содержит ключевые слова](../images/spd15-TitleFieldKeywords-visio.JPG)|Это условие Visio  это то же, что условие **Название содержит ключевые слова** в SharePoint Designer 2013 и отображается как: <br/> ![Если поле заголовка содержит ключевые слова](../images/spd15-TitleFieldKeywords-txt.JPG)|**Поле заголовка содержит ключевые слова** <br/> Это условие проверяет, если поле **заголовка** элемента содержит конкретное слово. Ключевое слово можно указать в Построитель строк. Это может быть статическое значение или динамической строки или сочетание код или вставить подстановки для поля или переменной. <br/> **Примечание:** Не удается найти более одного ключевого слова в условии **Название содержит ключевые слова** . Тем не менее, можно использовать логические операторы, такие как **||**(или) или **&amp;&amp;** (и.          |
   

### <a name="document-set-conditions"></a>Условия набора документов

Некоторые условия бизнес-процессов доступны только сопоставлен рабочий процесс для библиотеки документов, таких как Общие документы или типа контента документа.
  
    
    


|**ФИГУРА УСЛОВИЯ VISIO**|**СООТВЕТСТВУЮЩИЙ УСЛОВИЕ В SHAREPOINT DESIGNER**|**ОПИСАНИЕ УСЛОВИЯ**|
|:-----|:-----|:-----|
|![Размер файла находится в определенном диапазоне](../images/spd15-FileSzInSpecRange-visio.JPG)|Это условие Visio  это то же, что **размер файла в конкретном диапазоне Кбайт** условие в SharePoint Designer 2013 и отображается как: <br/> ![Размер файла находится в определенном диапазоне](../images/spd15-FileSzInSpecRange-txt.JPG)|**Размер файла находится в определенном диапазоне** <br/> Это условие проверяет, если размер файла документа находится в пределах указанного размера, в килобайтах. Условие не включает указанного размера в расчет. Можно ввести номер или использовать подстановки для первого или второго размера в условии.<br/> |
|![Файл имеет определенный тип](../images/spd15-FileIsSpecType-visio.JPG)|Это условие Visio  это то же, что **файл имеет конкретный тип** условия в SharePoint Designer 2013 и отображается как: <br/> ![Файл имеет определенный тип](../images/spd15-FileIsSpecType-txt.JPG)|**Файл имеет определенный тип** <br/> Это условие проверяет, является ли тип файла текущего элемента указанного типа, например, docx. Можно ввести тип файла в виде строки или использовать подстановки.<br/> |
   

### <a name="list-conditions"></a>Список условий


  
    
    




|**ФИГУРА УСЛОВИЯ VISIO**|**СООТВЕТСТВУЮЩИЙ УСЛОВИЕ В SHAREPOINT DESIGNER**|**ОПИСАНИЕ УСЛОВИЯ**|
|:-----|:-----|:-----|
|![Проверка явных разрешений пользователя](../images/spd15-ChkExactUserPerms-visio.JPG)|Это условие Visio  это то же, что условие **Проверить уровни разрешений для элемента списка** в SharePoint Designer 2013 и отображается как: <br/> ![Проверка уровней разрешений для элемента списка](../images/spd15-ChkExactUserPerms-txt.JPG)|**Проверка явных разрешений пользователя** <br/> Это условие проверяет, что указанный пользователь обладает уровнем минимальные необходимые разрешения.  <br/> |
|![Проверка разрешений пользователя](../images/spd15-ChkUserPerms-visio.JPG)|Это условие Visio  это то же, что условие **проверять разрешения для элемента списка** в SharePoint Designer 2013 и отображается как: <br/> ![Проверка разрешений для элемента списка](../images/spd15-ChkUserPerms-txt.JPG)|**Проверка разрешений пользователя** <br/> Это условие проверяет наличие минимальные разрешения, необходимые для указанного пользователя.  <br/> |
   

## <a name="workflow-terminators"></a>Знаки завершения рабочего процесса
<a name="section3"> </a>

В Visio каждый рабочий процесс должен начинаться с конца Start (![Начало](../images/spd15-WFStart-icon.JPG)) и заканчиваться с конца Stop (![Остановка](../images/spd15-WFStop-icon.JPG)). Можно использовать только один из каждого типа терминатор для заданного рабочего процесса. Признаки конца необходимы для создания рабочих процессов SharePoint в Visio, чтобы рабочий процесс может пройти проверку и можно экспортировать. Знаки завершения рабочего процесса в SharePoint Designer не используются.
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Что нового в рабочих процессах для SharePoint](what-s-new-in-workflows-for-sharepoint.md)
    
  
-  [Общие сведения о рабочих процессах в SharePoint](get-started-with-workflows-in-sharepoint.md)
    
  
-  [Разработка рабочих процессов в SharePoint Designer и Visio](workflow-development-in-sharepoint-designer-and-visio.md)
    
  

  
    
    