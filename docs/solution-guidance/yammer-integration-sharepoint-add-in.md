---
title: "Интеграция Yammer в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: a83623a32b398ae32ce7cebc7ac5d37c823a2e3f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="yammer-integration-in-the-sharepoint-add-in-model"></a>Интеграция Yammer в объектная модель SharePoint
=================================================

<a name="summary"></a>Summary
-------

Выбор подхода к интеграции сети Yammer с помощью SharePoint аналогична в новой модели надстройки SharePoint как есть с кодом полного доверия.

<a name="high-level-guidelines"></a>Рекомендации по высокого уровня
---------------------

Как правило эскиз мы предлагаем для обеспечения высокого уровня следующее интеграции сети Yammer с SharePoint.

- Yammer интеграции может использоваться в локальной и среды Office 365 SharePoint.
- Удаленный подготовки шаблон можно использовать для создания группы Yammer и/или Yammer OpenGraph объекты для упрощения бесед при создании новых сайтов SharePoint.
- Можно использовать-стандартной внедрить возможность быстро и легко интеграции сети Yammer с SharePoint.
    + Для использования внедрить вы должны контейнер 400 пикселей HTML и более в приложении.
- Yammer пакеты SDK и API-интерфейсы REST можно использовать для создания настраиваемой интеграции функций.

<a name="options-to-integrate-yammer-with-sharepoint"></a>Параметры для интеграции сети Yammer с SharePoint
-------------------------------------------

У вас есть несколько вариантов для интеграции сети Yammer с SharePoint.

- Внедрить
    + Группа, тема, My и каналы новостей пользователей
    + OpenGraph веб-каналов
- Yammer OpenGraph API и/или интерфейса API REST Yammer с Yammer пакеты SDK
    
<a name="embed"></a>Внедрить
-----

В этом параметре внедрять Yammer, веб-канал на веб-странице SharePoint.
    
- Этот параметр, быстро и легко реализуется.
- Этот параметр позволяет управлять ограниченный аспектов веб-канал и как он находится.

На странице SharePoint с помощью внедрить выглядит следующим образом:

![Стандартные страницы сайта SharePoint team с текстовое поле, которое содержит текст, начать беседу. Ниже текста поле — это список, отображающий поток беседы Yammer.](media/Recipes/Yammer/YammerEmbed.png)

В следующей таблице описываются каждого типа ожидания введите встраивания веб-канал, чтобы воспользоваться с Yammer.

Веб-канала | Описание | FeedType | Пример использования
---- | ----------- | -------- | --------
Мой канал | Веб-каналов, где будут доставляться беседы для пользователей Yammer. | MyFeed | Сайт главной страницы или рабочей области сайте.
Веб-канал пользователя | Все беседы, размещенные отдельного пользователя в сети Yammer. | пользователь; | Страницы профилей пользователей в каталоге системы.
Раздел веб-канал | Канал бесед, которые помечены раздел в Yammer. | Раздел | На странице событий во внутренней сети.
Канал группы | Канал бесед, которые были учтены в указанной группы. | Group | Страница группы во внутренней сети.

Если вам потребуется за пределы возможностей каналы Yammer вне поля в таблице, можно использовать OpenGraph могут внедрять параметр.  Этот параметр позволяет управлять веб-канала.  В следующей таблице показан пример.

Веб-канала | Описание | FeedType | Пример использования
---- | ----------- | -------- | --------
Комментарий веб-канал | Используется в Yammer диаграммы прикладной программный Интерфейс для облегчения беседы вокруг объекта приложения. | Пользовательский | Возможность в мультимедиа или пользовательского приложения CRM странице сведений в системе управления цифровыми активами.

**Когда это подходит?**

При попытке интегрировать каналы Yammer с сайтами SharePoint и возможности ожидания введите канал embed соответствии со своими потребностями.

**Приступая к работе**

Следующий пример демонстрирует Подготовка сайтов с помощью канала Yammer узла вместо новостей по умолчанию для сайта.

- [Provisioning.Yammer (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Yammer)

Метод **CreateYammerGroupDiscussionPartXml** в классе [YammerUtility.cs](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Utilities/YammerUtility.cs) , поступающие из примера [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/OfficeDevPnP.Core) .  Этот метод создает XML-код для определения части Add-in, который добавляется на страницу SharePoint при подготовке сайта.  Уведомление о **feedType: «группа»** фрагмента кода.  Здесь можно увидеть, что feedType настроена на использование feedType ожидания введите группы.

    public static string CreateYammerGroupDiscussionPartXml(string yammerNetworkName, int yammerGroupId, bool showHeader, bool showFooter, bool useSSO = true)
    {
        StringBuilder wp = new StringBuilder(100);
        wp.Append("<?xml version=\"1.0\" encoding=\"utf-8\" ?>");
        wp.Append("<webParts>");
        wp.Append(" <webPart xmlns='http://schemas.microsoft.com/WebPart/v3'>");
        wp.Append("     <metaData>");
        wp.Append("         <type name='Microsoft.SharePoint.WebPartPages.ScriptEditorWebPart, Microsoft.SharePoint, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c' />");
        wp.Append("         <importErrorMessage>Cannot import this Web Part.</importErrorMessage>");
        wp.Append("     </metaData>");
        wp.Append("     <data>");
        wp.Append("         <properties>");
        wp.Append("             <property name='Title' type='string'>$Resources:core,ScriptEditorWebPartTitle;</property>");
        wp.Append("             <property name='Description' type='string'>$Resources:core,ScriptEditorWebPartDescription;</property>");
        wp.Append("             <property name='ChromeType' type='chrometype'>None</property>");
        wp.Append("             <property name='Content' type='string'>");
        wp.Append("             <![CDATA[");
        wp.Append("                 <div id='embedded-feed' style='height: 500px;'></div>");
        wp.Append("                 <script type='text/javascript' src='https://assets.yammer.com/assets/platform_embed.js'></script>");
        wp.Append("                 <script type='text/javascript'>  
                                        yam.connect.embedFeed({ container: '#embedded-feed', network: '"
                                        + yammerNetworkName
                                        + @"', feedType: 'group', feedId: '" + yammerGroupId            
                                        + @"', config: { use_sso: " + useSSO.ToString().ToLower()           
                                        + @", header: " + showHeader.ToString().ToLower()
                                        + @", footer: " + showFooter.ToString().ToLower()
                                        + " }}); </script>");
        wp.Append("             ]]>");
        wp.Append("             </property>");
        wp.Append("         </properties>");
        wp.Append("     </data>");
        wp.Append(" </webPart>");
        wp.Append("</webParts>");

        return wp.ToString();
    }

Метод **CreateYammerOpenGraphDiscussionPartXml** в классе [YammerUtility.cs](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Utilities/YammerUtility.cs) , поступающие из примера [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/OfficeDevPnP.Core) .  Этот метод создает XML-код для определения части Add-in, который добавляется на страницу SharePoint при подготовке сайта.  Уведомление о **feedType: «открыть график»** фрагмента кода.  Здесь можно увидеть, что feedType настроена на использование OpenGraph API.

    public static string CreateYammerOpenGraphDiscussionPartXml(string yammerNetworkName, string url, bool showHeader, 
                                                                    bool showFooter, string postTitle="", string postImageUrl="", 
                                                                    bool useSso = true, string groupId = "")
        {
            StringBuilder wp = new StringBuilder(100);
            wp.Append("<?xml version=\"1.0\" encoding=\"utf-8\" ?>");
            wp.Append("<webParts>");
            wp.Append(" <webPart xmlns='http://schemas.microsoft.com/WebPart/v3'>");
            wp.Append("     <metaData>");
            wp.Append("         <type name='Microsoft.SharePoint.WebPartPages.ScriptEditorWebPart, Microsoft.SharePoint, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c' />");
            wp.Append("         <importErrorMessage>Cannot import this Web Part.</importErrorMessage>");
            wp.Append("     </metaData>");
            wp.Append("     <data>");
            wp.Append("         <properties>");
            wp.Append("             <property name='Title' type='string'>$Resources:core,ScriptEditorWebPartTitle;</property>");
            wp.Append("             <property name='Description' type='string'>$Resources:core,ScriptEditorWebPartDescription;</property>");
            wp.Append("             <property name='ChromeType' type='chrometype'>None</property>");
            wp.Append("             <property name='Content' type='string'>");
            wp.Append("             <![CDATA[");
            wp.Append("                 <div id='embedded-feed' style='height: 500px;'></div>");
            wp.Append("                 <script type='text/javascript' src='https://assets.yammer.com/assets/platform_embed.js'></script>");
            wp.Append("                 <script>");
            wp.Append("                     yam.connect.embedFeed({");
            wp.Append("                       container: '#embedded-feed'");
            wp.Append("                             , feedType: 'open-graph'");
            wp.Append("                             , feedId: ''");
            wp.Append("                             , config: {");
            wp.Append("                                  use_sso: " + useSso.ToString().ToLower());
            wp.Append("                                  , header: " + showHeader.ToString().ToLower());
            wp.Append("                                  , footer: " + showFooter.ToString().ToLower());
            wp.Append("                                  , showOpenGraphPreview: false");
            wp.Append("                                  , defaultToCanonical: false");
            wp.Append("                                  , hideNetworkName: false");
            wp.Append("                                  , promptText: 'Start a conversation'");
            if (!string.IsNullOrEmpty(groupId))
            {
                wp.Append("                              , defaultGroupId: '" + groupId + "'"); 
            }
            wp.Append("                             }");
            wp.Append("                             , objectProperties: {"); 
            wp.Append("                               url: '" + url + "'");
            wp.Append("                               , type: 'page'");
            wp.Append("                               , title: '" + postTitle + "'");
            wp.Append("                               , image: '" + postImageUrl + "'");
            wp.Append("                             }");
            wp.Append("                         });");
            wp.Append("                     </script>");
            wp.Append("             ]]>");
            wp.Append("             </property>");
            wp.Append("         </properties>");
            wp.Append("     </data>");
            wp.Append(" </webPart>");
            wp.Append("</webParts>");

            return wp.ToString();
        }

Просмотрите [интеграции Yammer веб-каналов для сайтов SharePoint (O365 PnP видео)](https://channel9.msdn.com/blogs/OfficeDevPnP/Integrate-Yammer-feeds-to-SharePoint-sites) для просмотра прохода of - [Provisioning.Yammer (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Yammer).

Для внедрения Дополнительные сведения о сети Yammer в статье [Yammer внедрения веб-канала (Yammer центр для разработчиков)](https://developer.yammer.com/v1.0/docs/embed) .

Дополнительные сведения о Yammer OpenGraph в статье [Open Общие сведения о графике & Формат (Yammer центр для разработчиков)](https://developer.yammer.com/v1.0/docs/open-graph) .

<a name="yammer-opengraph-api--yammer-rest-api-with-yammer-sdks"></a>Yammer OpenGraph API & API-Интерфейс REST Yammer с Yammer пакеты SDK
-------------------------------------------------------

В этом параметре используется Yammer OpenGraph API и/или интерфейса API REST Yammer с Yammer пакеты SDK для интеграции сети Yammer с помощью SharePoint.  Эти API-интерфейсы также могут быть использованы для интеграции сети Yammer с процессами за пределами веб-страниц.  Такие сценарии примеры служб и длительной операции. 
    
- Этот параметр занимает больше времени для реализации.
- Этот параметр позволяет управлять все аспекты веб-канал и как оно отображается и взаимодействия с ним.

**Когда это подходит?**

- Когда вы пытаетесь интегрировать каналы Yammer с сайтами SharePoint и ожидания введите возможности веб-каналов embed не отвечают вашим требованиям.
- Когда вы пытаетесь интеграции каналы Yammer в служб или длительной операции.

**Приступая к работе**

Дополнительные сведения о Yammer OpenGraph в статье [Open Общие сведения о графике & Формат (Yammer центр для разработчиков)](https://developer.yammer.com/v1.0/docs/open-graph) .

Пакеты SDK для Yammer дают возможность проходить проверку подлинности в сети Yammer.  Дополнительные сведения о SDK Yammer увидеть следующие статьи:

- [Пакет SDK для JavaScript](https://developer.yammer.com/v1.0/docs/js-sdk)
- [Произносится SDK](https://developer.yammer.com/v1.0/docs/ruby-sdk)
- [Python SDK](https://developer.yammer.com/v1.0/docs/python-sdk)
- [пакет SDK для iOS](https://developer.yammer.com/v1.0/docs/ios-sdk)
- [ПАКЕТ SDK ДЛЯ .NET](https://developer.yammer.com/v1.0/docs/net-sdk)
- [Windows Phone 8 SDK](https://developer.yammer.com/v1.0/docs/windows-phone-8-sdk)

После проверки подлинности в Yammer с помощью SDK Yammer можно вызывать API REST Yammer.  

Дополнительные сведения о Yammer API-интерфейсы REST в статье [API -Интерфейс REST & ограничения скорости (Yammer центр для разработчиков)](https://developer.yammer.com/v1.0/docs/rest-api-rate-limits) .

**Примечание проверки подлинности**

В сценарии, где входа в SharePoint с использованием учетных данных, которые отличаются от учетных данных, используемые для входа в SharePoint с помощью вы можете разработать функцию единого входа для пользователей.  Пример такой ситуации — при входе в SharePoint с помощью LiveID и нужно входить в Yammer с Microsoft личных или рабочих учетной записи.

Для реализации сценария single sign on может направлять пользователей для входа в Yammer при первом они поступают на страницу SharePoint с помощью настраиваемого компонента Yammer на нем. После входе пользователя в сети Yammer с помощью пакета SDK Yammer можно хранить маркер обновления для пользователя в своем профиле пользователя.  Затем на последующих посещений страницы можно получить маркер обновления из профиля пользователя и используйте его для проверки подлинности.  При использовании этого подхода конечных пользователей, достаточно для входа в Yammer при истечении срока действия маркера их обновления.

<a name="related-links"></a>Ссылки по теме
=============
- [Интеграция веб-каналы Yammer на сайтах SharePoint (O365 PnP видео)](https://channel9.msdn.com/blogs/OfficeDevPnP/Integrate-Yammer-feeds-to-SharePoint-sites)
- [Yammer внедрения веб-канал (Yammer центр для разработчиков)](https://developer.yammer.com/v1.0/docs/embed)
- [Общие сведения о графике Open & Формат (Yammer центр для разработчиков)](https://developer.yammer.com/v1.0/docs/open-graph)
- Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")
- Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")
- Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")

<a name="related-pnp-samples"></a>Примеры связанных с ними PnP
===================
- [Provisioning.Yammer (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Yammer)
- [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core)
- Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Применимо к
==========
- Office 365 нескольких клиентов (MT)
- Office 365 выделенных (D)
- SharePoint 2013 в локальной
