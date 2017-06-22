# <a name="set-up-your-office-365-tenant"></a>Настройка клиента Office 365

Для создания и развертывания клиентских веб-частей с помощью предварительного выпуска платформы SharePoint Framework необходим обычный клиент Office 365. 

## <a name="sign-up-for-an-office-365-tenant"></a>Регистрация клиента Office 365
Если у вас уже есть клиент Office 365, переходите к разделу [Создание сайта каталога приложений](#create-app-catalog-site).

В противном случае вы можете создать клиент пробной версии или принять участие в [программе для разработчиков Office](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=7a6e3d71-b057-49cc-b2aa-158ff23432f3&lcid=1033&culture=en-us&dir=LTR). Вы получите по электронной почте сообщение с приветствием и ссылкой, позволяющей зарегистрировать клиент разработчика приложений для Office 365. 

>**Примечание.** Перед регистрацией убедитесь, что вы вышли из всех имеющихся клиентов Office 365.

## <a name="create-app-catalog-site"></a>Создание сайта каталога приложений
Для отправки и развертывания веб-частей необходим каталог приложений. Если вы уже настроили каталог приложений, переходите к разделу [Создание коллекции сайтов разработчиков](#create-a-new-developer-site-collection).  

Откройте **Центр администрирования SharePoint**, указав в браузере приведенный ниже URL-адрес. Замените **yourtenantprefix** префиксом клиента разработчика приложений для Office 365.
    
```
https://yourtenantprefix-admin.sharepoint.com
```
    
На боковой панели слева выберите пункт меню **Приложения**, а затем — **Каталог приложений**.

Нажмите кнопку **ОК**, чтобы создать сайт каталога приложений.

На следующей странице введите указанные ниже сведения.

* **Название**: введите **Каталог приложений**.
* **_Суффикс_ адреса веб-сайта**: введите предпочитаемый суффикс каталога приложений, например **apps**.
* **Администратор**: введите имя пользователя и нажмите кнопку **Разрешить**, чтобы разрешить его.

Нажмите кнопку **ОК**, чтобы создать сайт каталога приложений.

SharePoint создаст сайт каталога приложений, а вы сможете наблюдать за ходом создания в Центре администрирования SharePoint.

## <a name="create-a-new-developer-site-collection"></a>Создание семейства сайтов разработчиков
Для тестирования также понадобится семейство веб-сайтов и сайт. Семейство веб-сайтов можно создать с помощью любого из доступных шаблонов. Мы можете использовать **семейство сайтов разработчиков**, но это излишне, так как базовое тестирование и тестирование в рабочей области можно выполнять на любом сайте.

Ниже приведены шаги, позволяющие создать семейство сайтов разработчиков.

 Откройте **Центр администрирования SharePoint**, указав в браузере приведенный ниже URL-адрес. Замените **yourtenantprefix** префиксом клиента разработчика приложений для Office 365.
    
```
https://yourtenantprefix-admin.sharepoint.com
```
    
На ленте SharePoint выберите команды **Создать** -> **Частное семейство веб-сайтов**.

В диалоговом окне введите указанные ниже сведения.

* **Название**: введите название семейства сайтов разработчиков, например **Сайт разработчика**.
* **_Суффикс_ адреса веб-сайта**: введите суффикс семейства сайтов разработчиков, например **dev**.
* **Выбор шаблона**: выберите для семейства веб-сайтов шаблон **Сайт разработчика**.
* **Администратор**: введите имя пользователя и нажмите кнопку **Разрешить**, чтобы разрешить его.

Нажмите кнопку **ОК**, чтобы создать семейство веб-сайтов.

SharePoint создаст сайт разработчика, а вы сможете наблюдать за ходом создания в Центре администрирования SharePoint. После создания сайта вы можете перейти к семейству сайтов разработчиков.

## <a name="sharepoint-workbench"></a>SharePoint Workbench
SharePoint Workbench — это рабочая область конструирования для разработчиков, которая позволяет быстро просматривать и проверять веб-части, не развертывая их в SharePoint. Цепочка инструментов для разработчиков, доступная в SharePoint Framework, включает локальную версию рабочей области, позволяющую быстро протестировать и проверить создаваемые решения. Эта область размещается также в области клиентов, чтобы вы могли просматривать и проверять локальные веб-части, которые находятся в разработке. Получить доступ к SharePoint Workbench можно на любом сайте SharePoint в своей области клиентов, перейдя по такому URL-адресу:

```
https://your-sharepoint-site/_layouts/workbench.aspx
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы настроили клиент SharePoint, [настройте среду разработки](./set-up-your-development-environment) для сборки клиентских веб-частей.