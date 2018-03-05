---
title: "Развертывание расширения в SharePoint (Hello World, часть 3)"
description: "Разверните настройщик заполнителей SharePoint Framework в SharePoint и проверьте, работает ли он на современных страницах SharePoint."
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: be5d91493d9425f158755364947b84b02dbfb487
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="deploy-your-extension-to-sharepoint-hello-world-part-3"></a>Развертывание расширения в SharePoint (Hello World, часть 3)

В этой статье рассказывается, как развернуть настройщик заполнителей SharePoint Framework в SharePoint и проверить, работает ли он на современных страницах SharePoint. 

Перед началом работы необходимо выполнить процедуры, описанные в следующих статьях:

* [Создание первого расширения SharePoint Framework (Hello World, часть 1)](./build-a-hello-world-extension.md)
* [Использование заполнителей страниц из настройщика заполнителей (Hello World, часть 2)](./using-page-placeholder-with-extensions.md)

Эти действия также показаны в видео на [канале SharePoint PnP на YouTube](https://www.youtube.com/watch?v=P_yWI0WVQIg&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV). 

<a href="https://www.youtube.com/watch?v=DzHdVxLA3Pc">
<img src="../../../images/spfx-ext-youtube-tutorial3.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="package-the-hello-world-application-customizer"></a>Упаковка настройщика заполнителей Hello World

1. В окне консоли перейдите в каталог проекта расширения, созданного при работе со статьей [Создание первого расширения SharePoint Framework (Hello World, часть 1)](./build-a-hello-world-extension.md).

  ```
  cd app-extension
  ```

2. Если команда gulp serve все еще выполняется, остановите ее, нажав клавиши CTRL+C.

  В отличие от работы в режиме **отладки**, чтобы использовать расширение на современных серверных страницах SharePoint, вам потребуется развернуть и зарегистрировать расширение в SharePoint в области `Site collection`, `Site` или `List`. Место и способ активации настройщика определяются областью. В данном сценарии мы зарегистрируем настройщик заполнителей, используя область `Site collection`. 

  Прежде чем упаковать решение, нам необходимо включить код для автоматизации активации решения при установке его на сайте. В данном случае мы воспользуемся элементами платформы компонентов, чтобы выполнить эти действия прямо в пакете решения, но вы, например, можете связать настройщик заполнителей с сайтом SharePoint, используя REST или CSOM при подготовке сайта к работе.

3. Установите пакет решения на нужном сайте, чтобы манифест расширения попал в список разрешенных для запуска.

4. Свяжите настройщик заполнителей с запланированной областью. Это можно сделать с помощью кода (CSOM/REST) или с помощью платформы компонентов в пакете решения SharePoint Framework. Указанные ниже свойства необходимо сопоставить в объекте `UserCustomAction` на уровне семейства веб-сайтов, сайта или списка.
  
  * **ClientSideComponentId** — идентификатор (GUID) настройщика полей, установленный в каталоге приложений. 
  * **ClientSideComponentProperties** — необязательный параметр, с помощью которого можно указать свойства для экземпляра настройщика полей.
   
  Обратите внимание, что вы можете требовать добавления вашего расширения на сайт, используя параметр `skipFeatureDeployment` в файле **package-solution.json**. Даже если вы не требуете установки решения на сайте, вам нужно связать идентификатор **ClientSideComponentId** с конкретными объектами, чтобы расширение было видимым. 
   
  На следующих этапах мы рассмотрим определение `CustomAction`, которое было автоматически создано для решения при формировании шаблонов для включения решения при его установке на сайте. 
   
5. Вернитесь к пакету решения в Visual Studio Code (или другом редакторе, который вы используете).

6. Разверните папку **sharepoint** и вложенную папку **assets** в корневой папке решения. Отобразится существующий файл **elements.xml**. 

   ![Папка assets в структуре решения](../../../images/ext-app-assets-folder.png)

<br/>

### <a name="review-the-existing-elementsxml-file-for-sharepoint-definitions"></a>Проверка наличия определений SharePoint в существующем файле elements.xml

Проверьте существующую XML-структуру в файле **elements.xml**. Обратите внимание, что свойство **ClientSideComponentId** было автоматически обновлено на основании уникального идентификатора вашего настройщика заполнителей, доступного в файле **HelloWorldApplicationCustomizer.manifest.json** в папке **src\extensions\helloWorld**.

Кроме того, для параметра **ClientSideComponentProperties** этого экземпляра расширения были автоматически заданы структура, используемая по умолчанию, и свойства JSON. Запомните, как выполняется выход из объекта JSON, чтобы мы могли правильно настроить его в XML-атрибуте. 

Для определения настройщика заполнителей в конфигурации используется конкретное расположение объекта `ClientSideExtension.ApplicationCustomizer`. Так как по умолчанию этот файл **elements.xml** сопоставлен с компонентом с областью *Интернет*, это действие `CustomAction` будет автоматически добавлено в коллекцию `Web.UserCustomAction` на сайте, на котором устанавливается решение.

Чтобы конфигурация соответствовала обновлениям, выполненным в настройщике заполнителей, измените параметр **ClientSideComponentProperties**, как показано в XML-структуре ниже. Учтите, что вам не следует копировать всю структуру, так как это приведет к расхождению с идентификатором **ClientSideComponentId**.


```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">

    <CustomAction 
        Title="SPFxApplicationCustomizer"
        Location="ClientSideExtension.ApplicationCustomizer"
        ClientSideComponentId="46606aa6-5dd8-4792-b017-1555ec0a43a4"
        ClientSideComponentProperties="{&quot;Top&quot;:&quot;Top area of the page&quot;,&quot;Bottom&quot;:&quot;Bottom area in the page&quot;}">

    </CustomAction>

</Elements>
```

<br/>

### <a name="ensure-that-definitions-are-taken-into-account-within-the-build-pipeline"></a>Сделайте так, чтобы определения учитывались при упаковке

Откройте файл **package-solution.json** в папке **config**. В файле **package-solution.json** определяются метаданные пакета, как показано в следующем фрагменте кода. Чтобы при упаковке решения учитывался файл **element.xml**, функция формирования шаблонов, используемая по умолчанию, добавляет необходимую конфигурацию, чтобы создать определение компонента платформы компонентов для пакета решения.

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
  "solution": {
    "name": "app-extension-client-side-solution",
    "id": "98a9fe4f-175c-48c1-adee-63fb927faa70",
    "version": "1.0.0.0",
    "features": [
      {
        "title": "Application Extension - Deployment of custom action.",
        "description": "Deploys a custom action with ClientSideComponentId association",
        "id": "4678966b-de68-445f-a74e-e553a7b937ab",
        "version": "1.0.0.0",
        "assets": {
          "elementManifests": [
            "elements.xml"
          ]
        }
      }
    ]
  },
  "paths": {
    "zippedPackage": "solution/app-extension.sppkg"
  }
}


```

<br/>

## <a name="deploy-the-extension-to-sharepoint-online-and-host-javascript-from-local-host"></a>Развертывание расширения в SharePoint Online и размещение кода JavaScript в локальном узле

Теперь мы готовы развернуть решение на сайте SharePoint и автоматически сопоставить действие `CustomAction` на уровне сайта.

1. Чтобы упаковать клиентское решение, содержащее расширение, и получить базовую структуру, готовую к упаковке, в окне консоли введите указанную ниже команду.

   ```
   gulp bundle
   ```

2. Затем выполните следующую команду, чтобы создать пакет решения:

   ```
   gulp package-solution
   ```

   Эта команда создает пакет в папке **sharepoint/solution**:

   ```
   app-extension.sppkg
   ```

3. Теперь необходимо развернуть пакет, созданный в каталоге приложений. Для этого перейдите в **каталог приложений** клиента и откройте библиотеку **Приложения для SharePoint**.

4. Отправьте или перетащите файл `app-extension.sppkg` из папки **sharepoint/solution** в каталог приложений. В SharePoint откроется диалоговое окно с запросом на подтверждение доверия клиентскому решению.

   Обратите внимание, что мы не изменяли URL-адреса для размещения решения в этом развертывании, поэтому по-прежнему используется URL-адрес `https://localhost:4321`. 
   
5. Нажмите кнопку **Развернуть**.

   ![Операция доверия при отправке в каталог приложений](../../../images/ext-app-sppkg-deploy-trust.png)

6. Вернитесь к консоли и убедитесь, что решение запущено. Если это не так, выполните в папке решения следующую команду:
   
   ```
   gulp serve --nobrowser
   ```
   
7. Перейдите на тот сайт, где требуется проверить подготовку ресурсов SharePoint. Это может быть любое семейство веб-сайтов в клиенте, где развернут пакет решения.

8. Щелкните значок с изображением шестеренки на верхней панели навигации справа и выберите команду **Добавить приложение**. Откроется страница "Приложения".

9. В поле **Поиск** введите **app**, а затем нажмите клавишу ВВОД, чтобы отфильтровать приложения.

   ![Установка настройщика полей на сайте](../../../images/ext-app-install-solution-to-site.png)

10. Выберите приложение **app-extension-client-side-solution**, чтобы установить решение на сайте. После завершения установки обновите страницу, нажав клавишу F5.

  После установки приложения верхний и нижний колонтитулы будут отрисовываться так же, как и при использовании параметров запроса отладки.

  ![Пользовательские элементы верхнего и нижнего колонтитулов на странице](../../../images/ext-app-header-footer-visible.png)

## <a name="next-steps"></a>Дальнейшие действия

Поздравляем, вы развернули расширение из каталога приложений на современной странице SharePoint! 

Из следующей статьи [Размещение расширения в сети доставки содержимого Office 365 (Hello World, часть 4)](./hosting-extension-from-office365-cdn.md) вы узнаете, как развернуть ресурсы расширения в сети CDN и загружать их оттуда.

> [!NOTE]
> Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues). Заранее спасибо!
