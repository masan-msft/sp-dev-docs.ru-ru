---
title: "Разработка с помощью клиента разрешения с помощью только для приложений в SharePoint Online"
ms.date: 11/03/2017
ms.openlocfilehash: 713483e18a9fa4248c4509c29c368863923c3854
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="developing-using-tenant-permissions-with-app-only-in-sharepoint-online"></a>Разработка с помощью клиента разрешения с помощью только для приложений в SharePoint Online

Опыт разработки для SharePoint **Add-ins, размещаемые у поставщика** , который требуется **разрешение клиента в сочетании с только для приложений**, была изменена. В этой статье описываются новые возможности для разработки и отладки эти решения. 

_**Применимо к:** Поставщик Add-ins for SharePoint Online_


## <a name="understanding-the-problem"></a>Общие сведения о проблемы
В Visual Studio выберите пункты отладка, начать отладку и сообщение об ошибке, «**Администратор клиента должен одобрить это приложение**» как показано ниже.
![](http://i.imgur.com/oFH9oqb.png). 

Причина, почему не удается щелкните **доверенным** том, что работы Visual Studio для разработчиков семейства веб-сайтов, указанный в параметры проекта, тогда как разрешения на уровне клиента с помощью только приложения могут быть предоставлены только через [доверие для вашего клиента сайт администрирования](https://msdn.microsoft.com/en-us/pnp_articles/how-to-provide-add-in-app-only-tenant-administrative-permissions-in-sharepoint-online).

## <a name="walkthrough"></a>Пошаговое руководство
### <a name="step-1-create-a-new-service-principal"></a>Шаг 1: Создание новых участников служб
Перейдите к семейству сайтов клиента и создание нового идентификатора клиента и секрет. (Например, https://contoso.sharepoint.com/_layouts/15/appregnew.aspx). На этой странице щелкните **Создать** для обоих **Идентификатор клиента**, **Секрет клиента** полей и предоставить оставшиеся поля. При разработке надстройки убедитесь, что использование localhost.com, включая порт, что домен приложения. Вы должны что-то вроде как ниже.

![](http://i.imgur.com/5CfHgFD.png)

### <a name="step-2-grant-tenant-permissions"></a>Шаг 2: Клиента предоставление разрешений
Чтобы выполнить это действие, необходимо быть администратором SharePoint Online. 

Перейдите в центр администрирования SharePoint (например, https://contoso-admin.sharepoint.com/_layouts/15/appinv.aspx) и предоставить разрешения клиента![](http://i.imgur.com/EGuJG3a.png)

![](http://i.imgur.com/dst9ZdP.png)


### <a name="step-3-update-your-manifest-and-webconfig"></a>Шаг 3: Обновление манифеста и файла web.config
В решении Visual Studio; обновление манифеста и файла web.config с идентификатором клиента, созданной на шаге 1.
![](http://i.imgur.com/fKkLIde.png)


### <a name="step-4-package-the-app-and-add-the-app-file-to-the-app-catalog"></a>Шаг 4: Упаковка приложения и добавьте App-файл в каталог приложений
Щелкните правой кнопкой мыши проект надстройки SharePoint и нажмите кнопку Опубликовать.

Укажите **Идентификатор клиента** и ** секрет клиента ** создан в шаге 1.

![](http://i.imgur.com/XpM9rwb.png)

Так как необходимо выполнить отладку надстройки, убедитесь, что вы задаете https://localhost.com включая номер порта, как показано ниже.
![](http://i.imgur.com/nQmSbPC.png)

Теперь развертывание надстройки в сайт каталога приложений.

### <a name="step-5-install-your-add-in-in-your-developer-site-collection"></a>Шаг 5: Установка надстройки в в семействе веб-сайтов для разработчиков

Перейдите на сайт разработчика и добавить приложение. Выберите команду **сведения о приложении**.
![](http://i.imgur.com/Aihr4r7.png)

Если вы выбрали на Плитка приложения, необходимо выберите команду «**Узнайте, почему**» и запросить вашего приложения![](http://i.imgur.com/DwWUkG0.png)

После отправки запроса состояния будет находиться в состоянии ожидания до администратор SharePoint или каталога приложений администратора одобряет запрос. Утверждение запроса, перейдите в каталог приложений, запросы приложений и утвердить запрос.

![](http://i.imgur.com/yZ8vNEc.png)

После запроса утвержден надстройки могут теперь установить.

![](http://i.imgur.com/PMitOEY.png)

### <a name="step-6-debug-your-add-in"></a>Шаг 6: Отладка надстройки
В Visual Studio щелкните правой кнопкой мыши веб-проект и выберите новый экземпляр начальном **отладки** . После запуска перейдите на свой сайт и запустите надстройку.

![](http://i.imgur.com/Y5vAlDr.png)

> [!NOTE] 
> - Если для какой-либо причине приложение упаковать файл изменений необходимо снова развернуть ее в каталог приложений и повторно установить для семейства веб-сайтов разработки
> - Если вы надстройки имеет приемника событий appinstalled, необходимо убедиться, что вы сделали шаг 6, прежде чем шаг 5


## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Надстройка только клиента административные разрешения для приложений в SharePoint Online](https://msdn.microsoft.com/en-us/pnp_articles/how-to-provide-add-in-app-only-tenant-administrative-permissions-in-sharepoint-online)
- [Разрешения для надстроек в SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp142383.aspx)
- [Изучите структуру манифеста надстройки и пакет надстройки для SharePoint](https://msdn.microsoft.com/en-us/library/office/fp179918.aspx)

