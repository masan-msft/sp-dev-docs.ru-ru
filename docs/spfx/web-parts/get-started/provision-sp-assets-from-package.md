# <a name="provisioning-sharepoint-assets-from-your-sharepoint-client-side-web-part"></a>Подготовка ресурсов SharePoint из клиентской веб-части SharePoint

В этой статье описывается подготовка ресурсов SharePoint в составе решения SharePoint Framework. Эти ресурсы развертываются на сайтах SharePoint при установке решения. Кроме того, в этой статье рассматриваются необходимые действия для установки возможных обновлений в составе новых версий пакета. Этот процесс идентичен обновлению надстроек.

## <a name="prerequisites"></a>Необходимые условия
Прежде чем изучать базовый порядок создания собственной клиентской веб-части, выполните следующие действия:

* [Создайте свою первую веб-часть](build-a-hello-world-web-part.md).
* [Подключитесь к SharePoint](connect-to-sharepoint.md). 

## <a name="resources"></a>Ресурсы
В приведенных ниже ресурсах вы найдете дополнительные сведения на темы, рассматриваемые в данном руководстве.

* [Подготовка ресурсов SharePoint с пакетом решения](../../toolchain/provision-sharepoint-assets)
* [Пример решения: развертывание ресурсов SharePoint в составе пакета SPFx](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-feature-framework)

## <a name="create-a-new-web-part-project"></a>Создание проекта веб-части

Создайте каталог проекта в любом расположении:

```
md asset-deployment-webpart
```

Перейдите к каталогу проекта:

```
cd asset-deployment-webpart
```
    
Создайте клиентскую веб-часть с помощью генератора Yeoman для SharePoint:

```
yo @microsoft/sharepoint
```

Когда появится запрос:

* оставьте имя решения **asset-deployment-webpart** и нажмите клавишу **ВВОД**;
* выберите вариант **Use the current folder** (Использовать текущую папку) для размещения файлов.

Далее вам потребуется указать определенные сведения о веб-части:

* оставьте выбранным параметр **No JavaScipt web framework** (Не использовать платформу веб-решений на базе JavaScript) по умолчанию и нажмите клавишу **ВВОД**, чтобы продолжить;
* введите имя **AssetDeployment** для веб-части и нажмите клавишу **ВВОД**;
* введите описание веб-части **AssetDeployment Web Part** и нажмите клавишу **ВВОД**; 

После этого Yeoman установит необходимые зависимости и сформирует шаблоны файлов решения. Это может занять несколько минут. При этом Yeoman также включит в проект веб-часть **AssetDeployment**.

Введите в консоли следующий код, чтобы открыть проект веб-части в Visual Studio Code:

```
code .
```

## <a name="create-folder-structure-for-your-sharepoint-assets"></a>Создание структуры папок для ресурсов SharePoint

Для начала необходимо создать папку **assets**, в которую мы поместим все ресурсы платформы компонентов, используемые для подготовки структур SharePoint при установке пакета.

* Создайте папку **sharepoint** в корневой папке решения.
* Создайте папку **assets**, вложенную в только что созданную папку **sharepoint**.

Структура решения должна быть такой, как на рисунке ниже.

![Снимок экрана с папкой assets, вложенной в папку sharepoint, в структуре решения](../../../../images/tutorial-feature-solution-initial-structure.png)

## <a name="create-feature-framework-files-for-initial-deployment"></a>Создание файлов платформы компонентов для начального развертывания
Для подготовки ресурсов SharePoint на сайтах с элементами платформы компонентов необходимо создать нужные XML-файлы в папке ресурсов. Пакеты решений SharePoint Framework поддерживают следующие элементы:

* поля и столбцы сайтов;
* типы контента;
* экземпляры списков;
* экземпляры списков с настраиваемой схемой.

На следующих этапах мы определим подготавливаемую структуру.

### <a name="add-elementxml-file-for-sharepoint-definitions"></a>Добавление файла element.xml для определений SharePoint
Создайте в папке **sharepoint\assets** файл **elements.xml**.

Скопируйте следующую структуру XML в файл **elements.xml**:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">

    <Field ID="{060E50AC-E9C1-4D3C-B1F9-DE0BCAC300F6}"
            Name="SPFxAmount"
            DisplayName="Amount"
            Type="Currency"
            Decimals="2"
            Min="0"
            Required="FALSE"
            Group="SPFx Columns" />

    <Field ID="{943E7530-5E2B-4C02-8259-CCD93A9ECB18}"
            Name="SPFxCostCenter"
            DisplayName="Cost Center"
            Type="Choice"
            Required="FALSE"
            Group="SPFx Columns">
        <CHOICES>
        <CHOICE>Administration</CHOICE>
        <CHOICE>Information</CHOICE>
        <CHOICE>Facilities</CHOICE>
        <CHOICE>Operations</CHOICE>
        <CHOICE>Sales</CHOICE>
        <CHOICE>Marketing</CHOICE>
        </CHOICES>
    </Field>

    <ContentType ID="0x010042D0C1C200A14B6887742B6344675C8B" 
            Name="Cost Center" 
            Group="SPFx Content Types" 
            Description="Sample content types from web part solution">
        <FieldRefs>
            <FieldRef ID="{060E50AC-E9C1-4D3C-B1F9-DE0BCAC300F6}" /> 
            <FieldRef ID="{943E7530-5E2B-4C02-8259-CCD93A9ECB18}" />
        </FieldRefs>
    </ContentType> 

    <ListInstance 
            CustomSchema="schema.xml"
            FeatureId="00bfea71-de22-43b2-a848-c05709900100"
            Title="SPFx List" 
            Description="SPFx List"
            TemplateType="100"
            Url="Lists/SPFxList">
    </ListInstance>

</Elements>
```

Сведения об этой структуре XML.
* Мы подготавливаем на сайте два поля, тип контента и экземпляр списка с настраиваемой схемой.
* Определения используют стандартную схему платформы компонентов, хорошо знакомую разработчикам SharePoint.
* Добавляемый тип контента ссылается на настраиваемые поля.
* Мы используем атрибут **CustomSchema** в элементе **ListInstance**, чтобы определить файл schema.xml file для подготовки списка. Таким образом, список все еще основан на стандартном шаблоне списка (в данном случае это обычный настраиваемый список 100), но мы можем создать альтернативное определение во время начальной подготовки.

> Дополнительные сведения об используемых структурах схемы см. в [документации по платформе компонентов](https://msdn.microsoft.com/ru-ru/library/office/ms460318(v=office.14).aspx) на сайте MSDN.

### <a name="add-schemaxml-file-for-defining-list-structure"></a>Добавление файла schema.xml для определения структуры списка
На предыдущем этапе мы ссылались на файл **schema.xml** в атрибуте **CustomSchema** элемента **ListInstance**, поэтому его потребуется включить в наш пакет. 

Создайте в папке **sharepoint\assets** файл **schema.xml**.

Скопируйте следующую структуру XML в файл **schema.xml**:

```xml
<List xmlns:ows="Microsoft SharePoint" Title="Basic List" EnableContentTypes="TRUE" FolderCreation="FALSE" Direction="$Resources:Direction;" Url="Lists/Basic List" BaseType="0" xmlns="http://schemas.microsoft.com/sharepoint/">
  <MetaData>
    <ContentTypes>
      <ContentTypeRef ID="0x010042D0C1C200A14B6887742B6344675C8B" />
    </ContentTypes>
    <Fields></Fields>
    <Views>
      <View BaseViewID="1" Type="HTML" WebPartZoneID="Main" DisplayName="$Resources:core,objectiv_schema_mwsidcamlidC24;" DefaultView="TRUE" MobileView="TRUE" MobileDefaultView="TRUE" SetupPath="pages\viewpage.aspx" ImageUrl="/_layouts/images/generic.png" Url="AllItems.aspx">
        <XslLink Default="TRUE">main.xsl</XslLink>
        <JSLink>clienttemplates.js</JSLink>
        <RowLimit Paged="TRUE">30</RowLimit>
        <Toolbar Type="Standard" />
        <ViewFields>
          <FieldRef Name="LinkTitle"></FieldRef>
          <FieldRef Name="SPFxAmount"></FieldRef>
          <FieldRef Name="SPFxCostCenter"></FieldRef>
        </ViewFields>
        <Query>
          <OrderBy>
            <FieldRef Name="ID" />
          </OrderBy>
        </Query>
      </View>
    </Views>
    <Forms>
      <Form Type="DisplayForm" Url="DispForm.aspx" SetupPath="pages\form.aspx" WebPartZoneID="Main" />
      <Form Type="EditForm" Url="EditForm.aspx" SetupPath="pages\form.aspx" WebPartZoneID="Main" />
      <Form Type="NewForm" Url="NewForm.aspx" SetupPath="pages\form.aspx" WebPartZoneID="Main" />
    </Forms>
  </MetaData>
</List>
```

Сведения о включенной структуре XML.
* Элемент **ContentTypeRef** ссылается на настраиваемый тип контента, развертываемый с помощью файла **elements.xml**.
* Элемент **FieldRef** ссылается на настраиваемые поля **SPFxAmount** и **SPFxCostCenter**.

> Дополнительные сведения об используемых структурах схемы можно найти в статье [Общие сведения о файлах Schema.xml](https://msdn.microsoft.com/ru-ru/library/office/ms459356(v=office.14).aspx) на сайте MSDN.

## <a name="ensure-that-definitions-are-taken-into-use-in-build-pipeline"></a>Проверка использования определений в конвейере сборки
Теперь мы создали необходимые структуры для автоматической подготовки ресурсов SharePoint при развертывании решения. Далее необходимо убедиться, что эти XML-файлы упакованы в файле решения.

Откройте файл **package-solution.json** из папки config. В файле **package-solution.json** определяются метаданные пакета, как показано в следующем фрагменте кода:

```json
{
  "solution": {
    "name": "asset-deployment-webpart-client-side-solution",
    "id": "31086065-dbdb-493f-b02e-7b7f97f45bd9",
    "version": "1.0.0.0"
  },
  "paths": {
    "zippedPackage": "solution/asset-deployment-webpart.sppkg"
  }
}
```

Чтобы убедиться, что новые файлы платформы компонентов учитываются при упаковке решения, необходимо включить определение компонента для пакета решения. Добавим определение JSON для нужного компонента в структуру решения, как показано в приведенном ниже фрагменте кода.

```json
{
  "solution": {
    "name": "asset-deployment-webpart-client-side-solution",
    "id": "31086065-dbdb-493f-b02e-7b7f97f45bd9",
    "version": "1.0.0.0",
    "features": [{
      "title": "asset-deployment-webpart-client-side-solution",
      "description": "asset-deployment-webpart-client-side-solution",
      "id": "523fe887-ced5-4036-b564-8dad5c6c6e24",
      "version": "1.0.0.0",
      "assets": {        
        "elementManifests": [
          "elements.xml"
        ],
        "elementFiles":[
          "schema.xml"
        ]
      }
    }]
  },
  "paths": {
    "zippedPackage": "solution/asset-deployment-webpart.sppkg"
  }
}

```

Сведения о добавленных определениях JSON.
* В принципе, пакет может включать несколько компонентов, так как объект **features** является коллекцией, но это не рекомендуется.
* В разделе elementManifests мы ссылаемся на файл **elements.xml**, чтобы он был правильно упакован в фактической структуре XML компонента как файл манифеста элемента.
* Определение может включать несколько файлов element.xml, которые будут выполняться в том же порядке, в котором они упоминаются в определении JSON. Как правило, не рекомендуется использовать несколько файлов element.xml, так как это сильно усложняет разработку. Вы можете определить все необходимые ресурсы в файле element.xml.

## <a name="deploy-and-test-asset-provisioning"></a>Развертывание и тестирование подготовки ресурсов
Теперь все готово к развертыванию решения в SharePoint. Так как в данном случае мы подготавливаем ресурсы непосредственно на сайтах SharePoint при установке решения, эту возможность невозможно протестировать на локальном или сетевом рабочем месте.

Чтобы упаковать клиентское решение, содержащее веб-часть, и получить базовую структуру, готовую к упаковке, введите в окне консоли указанную команду:

```
gulp bundle
```
Затем выполните следующую команду, чтобы создать пакет решения:

```
gulp package-solution
```
Эта команда создаст пакет в папке `sharepoint/solution`:

```
asset-deployment-webpart.sppkg
```
Прежде чем тестировать пакет в SharePoint, взглянем на стандартные структуры, созданные для пакета в определенных элементах платформы компонентов. Вернитесь к Visual Studio Code и разверните папку `sharepoint/solution/debug`, которая содержит необработанные структуры XML, включаемые в фактический пакет **sppkg**.

![Снимок экрана с папкой debug, вложенной в папку sharepoint, в структуре решения](../../../../images/tutorial-feature-solution-debug-folder.png)

Далее вам потребуется развернуть созданный пакет в каталоге приложений.

Перейдите к каталогу приложений вашего сайта.

Отправьте или перетащите файл asset-deployment-webpart.sppkg из папки `sharepoint/solution` в каталог приложений. В SharePoint откроется диалоговое окно с предложением разрешить развертывание клиентского решения.

![Диалоговое окно доверия для развертывания пакета решения](../../../../images/tutorial-feature-solution-trust-app-catalog.png)

> Примечание. SharePoint проверяет опубликованный пакет при его развертывании, а диалоговое окно доверия открывается, только если пакет допускается к развертыванию. Вы также можете просмотреть состояние этой проверки в столбце "Допустимый пакет приложения" каталога приложений.

Перейдите на тот сайт, где требуется проверить подготовку ресурсов SharePoint. Это может быть любое семейство веб-сайтов в клиенте, где развернут пакет решения. 

Нажмите значок шестеренки на верхней панели навигации справа и выберите команду **Добавить приложение**, чтобы перейти к странице "Приложения".

В **поле поиска** введите **deployment** и нажмите клавишу **ВВОД**, чтобы отфильтровать приложения. 

![Поиск приложения на сайте](../../../../images/tutorial-feature-solution-add-app.png)

Выберите приложение **asset-deployment-webpart-client-side-solution**, чтобы установить его на сайте. По завершении установки обновите страницу, нажав клавишу **F5**.

![Новый список SPFx List и приложение на странице содержимого сайта после подготовки решения](../../../../images/tutorial-feature-solution-provision-app.png)

Обратите внимание, что настраиваемый список **SPFx List** также был подготовлен на сайте при развертывании пакета решения.

Выберите **SPFx List**, чтобы перейти к списку.

![Представление по умолчанию для настраиваемого списка с дополнительными стандартными полями](../../../../images/tutorial-feature-solution-list-view.png)

Обратите внимание, что настраиваемые поля **Amount** и **Cost Center** автоматически отображаются в представлении списка по умолчанию. 

## <a name="define-upgrade-actions-for-new-version"></a>Определение действий по обновлению для новой версии
При создании новой версии решения SharePoint Framework может потребоваться внести некоторые изменения в подготовленные ресурсы SharePoint. При развертывании новой версии пакета вы можете воспользоваться поддержкой действий по обновлению, которую предоставляет платформа компонентов. 

Решения SharePoint Framework поддерживают следующие определения действий по обновлению из платформы компонентов:
* ApplyElementManifest
* AddContentTypeField

> Дополнительные сведения об определениях действий по обновлению в платформе компонентов см. в статье [Процедура обновления надстроек для SharePoint](https://msdn.microsoft.com/ru-ru/library/office/fp179904.aspx) на сайте MSDN.

### <a name="add-new-elementxml-file-for-the-new-version"></a>Добавление нового файла element.xml для новой версии
Вернитесь к своему решению в Visual Studio Code.

Создайте в папке **sharepoint\assets** файл **elements-v2.xml**.

Скопируйте приведенную ниже структуру XML в файл **elements-v2.xml**, в котором определяется новый подготавливаемый список SharePoint под названием **New List**.

```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">

    <ListInstance 
            FeatureId="00bfea71-de22-43b2-a848-c05709900100"
            Title="New List" 
            Description="New list provisioned from v2"
            TemplateType="100"
            Url="Lists/NewList">
    </ListInstance>

</Elements>
```
Нам также потребуется определение фактических действий по обновлению платформы компонентов, поэтому создайте в папке **sharepoint\assets** файл **upgrade-actions-v2.xml**

Скопируйте следующую структуру XML в файл **upgrade-actions-v2.xml**: Обратите внимание, что ссылка на GUID компонента в пути указывает на автоматически созданную папку, вложенную в папку `sharepoint/solution/debug`, и ее следует изменить в соответствии с вашим решением. Этот GUID также совпадает с идентификатором GUID компонента, который мы определили в файле **package-solution.json**.

```xml
<ApplyElementManifests>
      <ElementManifest Location="523fe887-ced5-4036-b564-8dad5c6c6e24\elements-v2.xml" />
</ApplyElementManifests>

```

### <a name="deploy-new-version-to-sharepoint"></a>Развертывание новой версии в SharePoint

Далее нам потребуется обновить версии решения и компонента, ответственного за подготовку ресурсов. 

> Номер версии решения указывает среде SharePoint, что доступна новая версия решения SharePoint Framework. Увеличение версии гарантирует, что действия по обновлению будут выполнены надлежащим образом при обновлении пакета решения на существующих сайтах.

Откройте файл **package-solution.json** из папки config и измените значения версий решения и компонента на "2.0.0.0". Кроме того, необходимо включить файл **elements-v2.xml** в раздел elementManifest и добавить элемент upgradeActions с указателем на только что созданный файл **upgrade-actions-v2.xml**. 

Ниже полностью представлен файл **package-solution.json** с необходимыми изменениями. Обратите внимание, что идентификаторы в вашем решении могут слегка отличаться от представленных здесь, так что сосредоточьтесь только на добавлении недостающих элементов.

```json
{
  "solution": {
    "name": "asset-deployment-webpart-client-side-solution",
    "id": "31086065-dbdb-493f-b02e-7b7f97f45bd9",
    "version": "2.0.0.0",
    "features": [{
        "title": "asset-deployment-webpart-client-side-solution",
        "description": "asset-deployment-webpart-client-side-solution",
        "id": "523fe887-ced5-4036-b564-8dad5c6c6e24",
        "version": "2.0.0.0",
        "assets": {
          "elementManifests": [
            "elements.xml",
            "elements-v2.xml"
          ],
          "elementFiles": [
            "schema.xml"
          ],
          "upgradeActions":[
            "upgrade-actions-v2.xml"
        ]
        }
      }]
  },
  "paths": {
    "zippedPackage": "solution/asset-deployment-webpart.sppkg"
  }
}
```
> Обратите внимание, что мы также добавили файл **elements-v2.xml** в раздел elementManifest. Это гарантирует, что при установке пакета версии 2.0 на чистом сайте результат будет таким же, как и при обновлении пакетов.

Чтобы повторно упаковать клиентское решение, содержащее веб-часть, и получить базовую структуру, готовую к упаковке, введите в окне консоли указанную команду:

```
gulp bundle
```
Затем выполните следующую команду, чтобы создать пакет решения:

```
gulp package-solution
```
Эта команда создаст новую версию пакета решения в папке `sharepoint/solution`. Обратите внимание: заглянув в папку `sharepoint/solution/debug`, вы можете легко убедиться, что обновленные XML-файлы включены в пакет решения.

Далее вам потребуется развернуть новую версию в каталоге приложений.

Перейдите к каталогу приложений вашего клиента.

Отправьте или перетащите файл asset-deployment-webpart.sppkg из папки `sharepoint/solution` в каталог приложений. SharePoint предложит вам подтвердить переопределение текущей версии.

![Вопрос о замене в каталоге приложений](../../../../images/tutorial-feature-solution-override-sppkg.png)

Нажмите кнопку **Заменить**, чтобы добавить последнюю версию в каталог приложений.

Обратите внимание, что в столбце "Версия приложения" для решения **asset-deployment-webpart-client-side-solution** теперь отображается значение "2.0.0.0".

![Увеличенная строка решения в каталоге приложений с обновленным номером версии](../../../../images/tutorial-feature-solution-version-2.png)

### <a name="update-existing-instance-in-the-site"></a>Обновление существующего экземпляра на сайте
Теперь, когда пакет в каталоге приложений обновлен, мы можем перейти к фактическому сайту с содержимым SharePoint и обновить существующий экземпляр.

Перейдите на сайт, где вы развернули первую версию решения SharePoint Framework.

Выберите пункт **О программе** в контекстном меню решения **asset-deployment-webpart-client-side-solution**

![Контекстное меню существующего пакета на сайте](../../../../images/tutorial-feature-solution-hover-menu.png)

Вы увидите текущие сведения об установленном решении SharePoint Framework. На этой странице также отображается текст "*Доступна новая версия этого приложения. Получите ее сейчас*", указывающий на наличие новой версии.

![Контекстное меню существующего пакета на сайте](../../../../images/tutorial-feature-solution-app-details.png)

Нажмите кнопку **ПОЛУЧИТЬ**, чтобы приступить к обновлению пакета.

![Состояние приложения на странице содержимого сайта меняется на "Обновление"](../../../../images/tutorial-feature-solution-updating-app.png)

Обновление может занять некоторое время, но когда надстройка снова вернется в обычное состояние, вы можете нажать клавишу **F5**, чтобы обновить страницу содержимого сайта и убедиться, что новый список успешно подготовлен при обновлении.

![Страница содержимого сайта с дополнительным списком New List](../../../../images/tutorial-feature-solution-new-list.png)

Теперь мы успешно обновили этот экземпляр до последней версии. Платформа компонентов используется для подготовки ресурсов SharePoint практически так же, как и для модели надстроек SharePoint. Основное отличие заключается в том, что ресурсы подготавливаются непосредственно на обычном сайте SharePoint, так как в решениях SharePoint Framework нет таких понятий, как приложение и сайт приложения. 
