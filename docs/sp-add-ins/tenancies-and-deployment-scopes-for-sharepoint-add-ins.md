
# <a name="tenancies-and-deployment-scopes-for-sharepoint-add-ins"></a>Области клиентов и области развертывания для надстроек SharePoint
 В этой статье рассказывается о концепции тенантностей и различиях между развертыванием надстроек SharePoint в области клиента и в веб-области.
 

 **Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 


## <a name="tenancies-and-add-in-scope"></a>Тенантности и область надстройки
<a name="AppScope"> </a>

SharePoint Клиент это набор семейств веб-сайтов либо в ферме SharePoint, либо в SharePoint Online. В SharePoint Online семейства веб-сайтов относятся к отдельной учетной записи клиента. В ферме SharePoint в качестве семейств веб-сайтов могут выступать все семейства сайтов в веб-приложении SharePoint или их подмножество. Семейства сайтов могут также представлять собой набор семейств сайтов из различных веб-приложений в ферме. У клиента, как и у веб-приложения SharePoint, может быть каталог Надстройка SharePoint.
 

 
Надстройка SharePoint имеет уровень надстройки. Два возможных уровня надстроек: уровень веб-сайтов иуровень клиента. Это различие не обусловлено внутренними свойствами надстройки, и вам, как разработчику, не нужно выбирать уровень установки надстройки. Решение принимается администраторами клиента и является побочным эффектом выбора способа установки. После отправки надстройки в каталог надстроек клиента она незамедлительно становится доступной для установки на каждом отдельном веб-сайте в рамках клиента. Надстройки, которые устанавливаются подобным образом, относятся к уровню веб-сайтов. Однако администраторы клиента могут выбрать другой вариант. Они могут выбрать пакетную установку надстройки в подмножестве веб-сайтов в рамках клиента. Надстройки, которые устанавливаются подобным образом, относятся к уровню клиента. Администратор клиента может указать, на какие веб-сайты устанавливается надстройка, с помощью списка управляемых путей, списка шаблонов сайтов или списка семейств веб-сайтов. Установленные пакетным способом надстройки может удалить только администратор клиента. Когда администратор клиента удаляет надстройку, она удаляется с каждого веб-сайта на уровне клиента. Пользователи не могут удалять надстройки, установленные пакетным способом, на отдельных веб-сайтах. Такой же принцип применяется и к обновлению такого надстройки: это может сделать только администратор клиента одновременно на всех веб-сайтах на уровне клиента, на которых установлена надстройка.
 

 
Если надстройка, включающая сайт надстройки, устанавливается пакетным способом, создается только один сайт надстройки, совместно используемый всеми хост-сайтами, на которые устанавливается надстройка. Сайт надстройки размещается в семействе веб-сайтов каталога надстроек организации.
 

 
При создании семейств веб-сайтов в тенантности надстройки, которые были установлены ранее в пакетном режиме, будут автоматически установлены в новом семействе веб-сайтов.
 

 

 **Примечание.** Не следует путать область надстройки с областью компонента. Область компонента определяет, где следует развертывать элементы в компоненте. Возможные варианты: **Farm** (Ферма), **WebApplication** (Веб-приложение), **Site** (Сайт, то есть семейство веб-сайтов) и **Web** (Интернет). Для компонентов (и для компонентов хост-сайта, и для компонентов в WSP-файле в пакете надстройки) в надстройках SharePoint разрешен только вариант **Web** (Интернет). Кроме того, не следует путать область надстройки с уровнями разрешений надстроек. Надстройки SharePoint могут запрашивать разрешения для всех или выбранных частей контента SharePoint на уровнях списка, Интернета, семейства веб-сайтов и тенантности. При установке надстройки с использованием области клиента надстройке не будут предоставлены разрешения, которые она не получила бы в другом случае. Кроме того, при этом не будут отменены ключевые положения модели безопасности SharePoint. Сведения о разрешениях для надстроек см. в статье [Разрешения для надстроек в SharePoint](add-in-permissions-in-sharepoint-2013).
 


## <a name="limitations-of-tenant-scoped-add-ins"></a>Ограничения для надстроек области клиента
<a name="Tenant"> </a>

Вам не удастся установить надстройки указанных ниже типов в пакетном режиме.
 

 

- Надстройки, которые содержат настраиваемое действие для ленты. (Разрешены настраиваемые действия, которые развертываются как пункты меню.)
    
 
- Надстройки, которые содержат веб-часть надстройки. 
    
 
Кроме того, учтите, что установка на уровне клиента не поддерживается в версии SharePoint Online в Office 365 для малого бизнеса расширенный.
 

 

## <a name="how-to-install-uninstall-and-update-an-add-in-on-multiple-websites-in-a-tenancy"></a>Установка, удаление и обновление надстройки на нескольких веб-сайтах в тенантности
<a name="Web"> </a>

Независимо от того, устанавливается ли надстройка из Магазин Office или из каталога надстроек, администраторы клиента могут установить ее на нескольких веб-сайтах клиента, а также удалить и обновить ее с помощью следующих процедур.
 

 

### <a name="to-install-a-sharepoint-add-in-to-multiple-websites"></a>Установка надстройки SharePoint на нескольких веб-сайтах


1. Перейдите на страницу **Содержимое сайта** веб-сайта корпоративного каталога.
    
 
2. Щелкните **Добавить надстройку** и установите надстройку так же, как и на любом другом веб-сайте SharePoint.
    
 
3. После установки надстройки наведите указатель мыши на ссылку надстройки на странице **Содержимое сайта**. Отобразится ссылка **…**.
    
 
4. Щелкните ссылку. Отобразится выноска.
    
 
5. В меню выберите пункт **Развертывание**.
    
 
6. Используйте открывшийся интерфейс развертывания для указания семейств веб-сайтов, в которых необходимо установить надстройку. Можно выполнять фильтрацию по управляемым путям, шаблонам сайтов и URL-адресам. Для фильтров действует логическое отношение "ИЛИ": надстройка устанавливается во всех семействах веб-сайтов, которые проходят один или больше фильтров.
    
 
7. Нажмите кнопку **OK**.
    
 

### <a name="to-uninstall-a-batch-installed-sharepoint-add-in"></a>Удаление надстройки SharePoint, установленной в пакетном режиме


1. Перейдите на страницу **Содержимое сайта** веб-сайта корпоративного каталога.
    
 
2. Наведите указатель мыши на ссылку надстройки на странице **Содержимое сайта**. Отобразится ссылка **…**.
    
 
3. Щелкните ссылку. Отобразится выноска.
    
 
4. В выноске нажмите кнопку **Удалить**.
    
 

### <a name="to-update-a-batch-installed-sharepoint-add-in"></a>Обновление надстройки SharePoint, установленной в пакетном режиме


1. Перейдите на страницу **Содержимое сайта** веб-сайта корпоративного каталога. Если для надстройки доступно обновление, возле нее появится сообщение с соответствующей ссылкой.
    
 
2. Щелкните ссылку, чтобы обновить надстройку.
    
 
3. Когда вам будет предложено утвердить запросы на разрешения для надстройки, щелкните **Доверять**.
    
 

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15tenancies_addlresources"> </a>


-  [Публикация надстроек SharePoint](publish-sharepoint-add-ins)
    
 
-  [Важные аспекты разработки и архитектуры для надстроек SharePoint](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)
    
 
-  [Развертывание и установка надстроек SharePoint: методы и параметры](deploying-and-installing-sharepoint-add-ins-methods-and-options)
    
 
-  [Процесс обновления надстроек SharePoint](sharepoint-add-ins-update-process)
    
 

