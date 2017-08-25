
# <a name="include-an-add-in-part-in-the-provider-hosted-add-in"></a>Добавление веб-части надстройки в надстройку, размещенную у поставщика
Узнайте, как настроить внешний вид удаленной веб-формы на странице SharePoint в надстройке SharePoint, размещаемой у поставщика.
 

 **Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 

Это шестая часть серии статей, посвященной основам разработки надстроек, размещаемых у поставщика. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и предыдущими статьями из этой серии.
 

-  [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [Настройка внешнего вида надстройки SharePoint, размещенной у поставщика](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel)
    
 
-  [Добавление настраиваемой кнопки в надстройку, размещенную у поставщика](include-a-custom-button-in-the-provider-hosted-add-in)
    
 
-  [Краткий обзор объектной модели SharePoint](get-a-quick-overview-of-the-sharepoint-object-model)
    
 
-  [Добавление операций записи SharePoint в надстройку, размещенную у поставщика](add-sharepoint-write-operations-to-the-provider-hosted-add-in)
    
 

 **Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых у поставщика, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с этой статьей. Кроме того, вы можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) и открыть файл BeforeAdd-inPart.sln.
 

В данной статье вы добавите особую веб-часть, называемую веб-частью надстройки, в Надстройка SharePoint. Веб-часть надстройки позволяет использовать форму заказа надстройки на странице SharePoint.
 

## <a name="create-the-add-in-part"></a>Создание веб-части надстройки


 

 

 **Примечание.** Параметры запускаемых проектов в Visual Studio обычно возвращаются к значениям по умолчанию каждый раз, когда вы заново открываете решение. Открывая пример решения, рассматриваемый в этой серии статей, всегда выполняйте следующие действия: щелкните правой кнопкой мыши узел решения в **обозревателе решений** и выберите пункт **Назначить запускаемые проекты**, а затем убедитесь, что для всех трех проектов в столбце **Действие** задано значение **Запуск**.
 


1. В **обозревателе решений** щелкните правой кнопкой мыши проект **ChainStore** и выберите **Добавить | Создать элемент**.
    
 
2. Выберите тип **Клиентская веб-часть (хост-сайт)**, присвойте ей имя Place Order (Размещение заказа), а затем нажмите кнопку **Добавить** ("клиентская веб-часть" — это еще одно название веб-части надстройки).
    
 
3. На следующей странице мастера выберите второй переключатель **Выберите или введите URL-адрес существующей веб-страницы для контента клиентской веб-части**.
    
 
4. В раскрывающемся списке выберите URL-адрес для страницы **OrderForm.aspx**, а затем нажмите кнопку **Готово**.
    
    К проекту будет добавлен файл elements.xml, в котором определяется веб-часть надстройки, который затем откроется.
    
 
5. В элементе **ClientWebPart** замените перечисленные ниже атрибуты на указанные значения.
    

|**Атрибут**|**Значение**|
|:-----|:-----|
|Название|Разместить заказ|
|Описание|Форма размещения заказа|
|DefaultHeight (Высота, используемая по умолчанию)|320|

    Leave all the other attributes with their defaults and save the file.
    
 

## <a name="run-the-add-in-and-test-the-add-in-part"></a>Запуск надстройки и тестирование веб-части надстройки


 

 

1. Нажмите клавишу F5, чтобы развернуть и запустить вашу надстройку. Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL в SQL Express. Кроме того, он создает временную установку надстройки на вашем тестовом сайте SharePoint и немедленно запускает ее. Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить надстройке необходимые разрешения.
    
 
2. Когда откроется начальная страница надстройки, сама надстройка уже будет развернута, а пользователи смогут добавлять веб-часть надстройки **Place Order** (Размещение заказа) в любую область веб-частей на любой странице SharePoint веб-сайта магазина в Гонконге. Чтобы добавить ее на начальную страницу, выполните указанные ниже действия.
    
      1. На расположенном в верхней части начальной страницы элементе управления хрома нажмите кнопку **Вернуться на сайт**. Откроется домашняя страница магазина в Гонконге.
    
 
  2. На ленте откройте вкладку **Страница** и нажмите кнопку **Изменить**.
    
 
  3. После перевода страницы в режим правки откройте вкладку **Вставка** на ленте и нажмите кнопку **Веб-часть надстройки** (она может по-прежнему называться **Веб-часть приложения**).
    
 
  4. В открывшемся элементе управления вставкой веб-части выберите веб-часть надстройки **Размещение заказа**. Элемент управления будет выглядеть примерно так, как показано ниже.
    
  ![Элемент управления вставкой веб-части SharePoint. Выделена веб-часть под названием "Размещение заказа". Ее имя и описание отображаются в поле справа.](../../images/aae61f89-2e9e-4808-8b0c-2439dad7c701.PNG)
 

 

 
  5. Щелкните какую-нибудь из зон веб-части на форме. Это необходимо, чтобы задать расположение для веб-части надстройки. 
    
 
  6. Нажмите кнопку **Добавить** на элементе управления вставкой веб-части. Веб-часть надстройки **Размещение заказа** будет добавлена в выбранную зону веб-частей.
    
 
  7. На ленте нажмите кнопку **Сохранить**.
    
 
3. Теперь форма заказа отобразится на странице. У нее будет такие же внешний вид и удобство использования, как и у остальной части страницы. Она должна выглядеть указанным ниже образом. 
    
  ![Веб-часть надстройки "Размещение заказа" на странице с текстовыми полями "Продукт", "Поставщик" и "Количество", а также кнопкой "Разместить заказ".](../../images/beae2e3c-c1f4-4334-8ab8-0c42252cb2a2.PNG)
 

 

 
4. Введите значения полей **Поставщик**, **Продукт** и **Количество**, а затем нажмите кнопку **Разместить заказ**. На первый взгляд ничего не произойдет, но при этом в корпоративную базу данных будет добавлен заказ. Кроме того, вы можете очистить поля веб-части надстройки, обновив страницу.
    
 
5. Нажимайте кнопку "Назад" в браузере, пока не вернетесь на начальную страницу надстройки "Сеть магазинов", а затем нажмите кнопку **Показать заказы**. В списке вы увидите ваш новый заказ.
    
 
6. Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.
    
 
7. Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуется отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.
    
 

## 
<a name="Nextsteps"> </a>

 Надстройка зависит от двух списков, которые вы создали вручную. Но мы не хотим, чтобы пользователи тоже вводили списки вручную. В следующей статье вы начнете работу над процессом автоматического создания этих списков. Первый основной этап создание настраиваемых обработчиков события установки надстройки: [Обработка событий надстройки в надстройке, размещаемой у поставщика](handle-add-in-events-in-the-provider-hosted-add-in)
 

 
