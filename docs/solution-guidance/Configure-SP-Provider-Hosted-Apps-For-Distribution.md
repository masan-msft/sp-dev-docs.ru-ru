---
title: "Настройка SharePoint у поставщика надстроек для распределения"
ms.date: 11/03/2017
ms.openlocfilehash: 82a1c046063dda3a612f96f70e5583d58ca9a505
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="configure-sharepoint-provider-hosted-add-ins-for-distribution"></a>Настройка SharePoint у поставщика надстроек для распределения

### <a name="summary"></a>Summary ###

На этой странице рассматриваются проблемы, которые могут возникнуть при совместном использовании SharePoint приложение с размещением у поставщика с другими разработчиками или при получении копии из системы управления версиями, такие как Team Foundation Server, Git или Visual Studio Online.

# <a name="configure-sharepoint-provider-hosted-add-ins-for-distribution"></a>Настройка SharePoint у поставщика надстроек для распределения

Все SharePoint у поставщика надстройки созданы с помощью Visual Studio 2013 включить NuGet пакет, который добавляет кода SharePoint и ссылки на веб-приложения, который выступает в качестве RemoteWeb для надстройки SharePoint. 

Пакет NuGet, добавляемые в проект веб-приложения в средств разработчика Office в Visual Studio не установлена в реестре пакета NuGet и таким образом попыток выполнить восстановление пакетов NuGet завершится ошибкой, так как он не удается найти нужный пакет.

## <a name="understanding-the-problem"></a>Общие сведения о проблемы ##

**Office Developer Tools для Visual Studio 2013**, версия 12.0.31105, добавляет пакет NuGet для веб-приложений создан как RemoteWeb для SharePoint у поставщика надстроек. Этот пакет **приложения для набора средств SharePoint Web**, добавляет следующих элементов в веб-проект:

- Сборки и ссылки на сборки SharePoint со стороны клиента объектной модели (CSOM)
- Файл кода `TokenHelper.cs` , которое поможет в процессе проверки подлинности для надстроек.
- Файл кода `SharePointContext.cs` , приводятся рекомендации по созданию, обслуживанию контексте SharePoint в веб-приложения.

Способ работы Visual Studio является, что или addins, обычно содержат локальную копию пакетов NuGet, разработчики не всегда имеют подключение к Интернету для загрузки пакеты NuGet. Устанавливаемый пакет средства включают имеет идентификатор **AppForSharePoint16WebToolkit**.

Когда проекты фиксируются в системе управления версиями, обычно пакеты не включены как часть фиксации, так как они могут добавлять много требования пространства дополнительного хранилища и без необходимости увеличьте размер пакета при обмена с другими разработчиками. Таким образом один из первой задачи разработчиков выполните действия после получения копии проекта из системы управления версиями — выполнить [Восстановление пакетов NuGet](http://docs.nuget.org/docs/reference/package-restore).

Проблема в том, что пакет с таким же Идентификатором не существует в реестре пакета NuGet; не найден пакет с Идентификатором **AppForSharePoint16WebToolkit**. Вместо этого точное того же пакета был добавлен в реестр пакетов NuGet как **AppForSharePointWebToolkit** ([http://www.nuget.org/packages/AppForSharePointWebToolkit](http://www.nuget.org/packages/AppForSharePointWebToolkit)) ** (*Обратите внимание на то нехватка "16" идентификатор*).

## <a name="preparing-a-sharepoint-provider-hosted-add-in-project-for-source-control--distribution"></a>Подготовка размещением у поставщика добавьте в проект SharePoint для системы управления версиями и рассылки ##

До обновления Office Developer Tools для Visual Studio 2013 для устранения этой проблемы рекомендуется для изменения проекта перед внесением системы управления версиями, независимо от того, при использовании сервера Team Foundation Server, Visual Studio Online, Git или любой другой решение.

После создания проекта, поиск в рамках проекта `packages.config` файл и выполните поиск пакета с Идентификатором **AppForSharePoint16WebToolkit**. Удаление и повторная установка пакета — безопасный способ обновления проекта.

Откройте **Консоль диспетчера пакетов** в Visual Studio и введите следующую команду для удаления пакета:

  ````powershell
  PM> Uninstall-Package -Id AppForSharePoint16WebToolkit
  ````

  > Если удалить создает ошибка, не удалось найти пакет, просто удалите ссылку пакета из `packages.config` файл вручную и сохранить изменения.

Теперь установите общедоступной версии пакета же NuGet из открытого реестра:

  ````powershell
  PM> Install-Package -Id AppForSharePointWebToolkit
  ````

----------

### <a name="related-links"></a>Ссылки по теме ###
- [NuGet: Приложения для набора средств веб-сайта SharePoint](http://www.nuget.org/packages/AppForSharePointWebToolkit)
- [NuGet: Восстановление пакетов](http://docs.nuget.org/docs/reference/package-restore)

### <a name="applies-to"></a>Применимо к ###
-  Office 365 нескольких клиентов (MT)
-  Office 365 выделенных (D)
-  SharePoint 2013 в локальной

### <a name="author"></a>Автор
Эндрю Коннелл - [@andrewconnell](https://twitter.com/andrewconnell)

### <a name="version-history"></a>История изменений ###
Версия  | Date | Примечания
---------| -----| --------
0,1  | 31 декабря 2014 г. | Первый черновик
