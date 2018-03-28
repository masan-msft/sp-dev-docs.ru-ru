---
title: Работа с внешними данными в SharePoint
description: Ресурсы и рекомендации по доступу к внешним данным и операциям с ними с помощью JavaScript на страницах надстроек SharePoint.
ms.date: 12/22/2017
ms.prod: sharepoint
ms.openlocfilehash: c7e2322384f4c3a70d7124eb2b6d7351612421b1
ms.sourcegitcommit: c57fc0e802661b0771f8b022964b6956ab4f6caf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2017
---
# <a name="work-with-external-data-in-sharepoint"></a>Работа с внешними данными в SharePoint

В надстройках SharePoint часто необходимо получить данные, предоставляемые удаленным веб-приложением или службой на странице или в компоненте SharePoint, и управлять ими. Так как пользовательский код не разрешен на серверах SharePoint, надстройка должна использовать для этой цели JavaScript. Модель для надстроек SharePoint предоставляет несколько вариантов доступа к удаленным данным и службам.

## <a name="use-the-sharepoint-cross-domain-javascript-library-to-access-external-data"></a>Использование междоменной библиотеки JavaScript в SharePoint для доступа к внешним данным

Междоменную библиотеку можно использовать для получения доступа к данным в вашем удаленном веб-приложении, если вы предоставляете пользовательскую страницу прокси, расположенную в удаленной инфраструктуре. Разработчик должен работать с настраиваемой логикой, например, механизмом аутентификации (если он существует) для удаленного приложения, и несет ответственность за реализацию пользовательской страницы прокси. Используйте междоменную библиотеку, если необходимо обмениваться данными между удаленным источником данных и страницей SharePoint на уровне клиента.

Сведения о том, как использовать библиотеку таким способом, см. в статье [Создание настраиваемой страницы прокси для междоменной библиотеки в SharePoint](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint.md).
 
> [!NOTE] 
> Междоменную библиотеку SharePoint также можно использовать в другом направлении, т. е. JavaScript на удаленных веб-страницах может использовать ее для доступа к данным в SharePoint. Дополнительные сведения о таком применении библиотеки см. в статье [Создание надстроек SharePoint, использующих междоменную библиотеку](creating-sharepoint-add-ins-that-use-the-cross-domain-library.md).

## <a name="use-the-sharepoint-web-proxy-to-access-external-data"></a>Доступ ко внешним данным с помощью веб-прокси SharePoint

Вы можете использовать веб-прокси, который предоставляется в клиентской объектной модели JavaScript, для доступа к удаленным данным. (Прокси также доступен в клиентской объектной модели (CSOM) .NET, но эту модель невозможно использовать в коде, работающем на серверах SharePoint.) 

При использовании веб-прокси вы передаете запрос инициализации в SharePoint. SharePoint в свою очередь запрашивает данные в определенной конечной точке и передает ответ обратно на вашу страницу. Используйте веб-прокси, если необходимо передавать информацию между удаленным источником данных и страницей SharePoint на уровне сервера.

Дополнительные сведения об использовании прокси см. в статье [Отправка запросов удаленной службе с помощью веб-прокси в SharePoint](query-a-remote-service-using-the-web-proxy-in-sharepoint.md).

## <a name="see-also"></a>Дополнительные ресурсы
<a name="SP15Workdata_AddRes"> </a>

- [Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
- [Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md)
- [Доступ к внешним данным с помощью REST в SharePoint](../general-development/how-to-access-external-data-with-rest-in-sharepoint.md)
- [Авторизация и аутентификация надстроек SharePoint](authorization-and-authentication-of-sharepoint-add-ins.md)
- [Использование операций запросов OData в запросах SharePoint REST](use-odata-query-operations-in-sharepoint-rest-requests.md) 
- [Хранение данных в надстройках SharePoint](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscap.md#Data)
- [Создание компонентов взаимодействия с пользователем в SharePoint](create-ux-components-in-sharepoint.md)
- [Разработка надстроек SharePoint](develop-sharepoint-add-ins.md)

    
 

