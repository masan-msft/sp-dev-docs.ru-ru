---
title: "Вызов Microsoft Graph с помощью класса GraphHttpClient"
description: "Используйте класс GraphHttpClient для вызова REST API Microsoft Graph с помощью методов get(), post() и fetch()."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: 898787fd3a9a2fa758b186a9ca9ae3627c579fa2
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="use-graphhttpclient-to-call-microsoft-graph"></a>Вызов Microsoft Graph с помощью класса GraphHttpClient

> [!IMPORTANT]
> Класс **GraphHttpClient** находится на этапе тестирования, и в него могут быть внесены изменения. Сейчас он не поддерживается для использования в рабочих средах.

Используйте класс **GraphHttpClient** для вызова REST API Microsoft Graph. Вы можете выполнять запросы GET, POST и PATCH, используя методы **get()**, **post()** и **fetch()**. В этой статье рассказывается, как создать веб-часть на основе класса **GraphHttpClient**, но вы можете использовать класс **GraphHttpClient** в любом клиентском коде в SharePoint Framework.

## <a name="retrieve-office-365-groups-using-a-get-call"></a>Получение групп Office 365 с помощью вызова GET

Вы можете использовать метод **get()** для совершения вызова REST к Microsoft Graph. В этом примере показано, как получить список групп Office 365. 

### <a name="create-a-new-web-part-project"></a>Создание проекта веб-части

1. Создайте каталог проекта в любом расположении. 

  ```
  mkdir hellograph-webpart
  ```

2. Перейдите к каталогу проекта.

  ```
  cd hellograph-webpart
  ```

3. Создайте веб-часть, запустив генератор Yeoman для SharePoint.

  ```
  yo @microsoft/sharepoint
  ```

4. Когда отобразится соответствующий запрос, выполните указанные ниже действия.

  * Введите имя решения **hellograph-webpart**.
  * В качестве расположения для размещения файлов выберите вариант **Использовать текущую папку**.
  * Когда отобразится соответствующий запрос, введите **д**, если вы хотите разрешить администратору клиента развертывать решение немедленно на всех сайтах, не запуская процесс развертывания компонентов или добавления приложений на сайтах.
  * В качестве типа клиентского компонента, который необходимо создать, выберите вариант **Веб-часть**.
  * В качестве имени веб-части введите **HelloGraph**.
  * В качестве описания веб-части введите **Вызов API Групп Microsoft Graph**.
  * Оставьте параметр **No javascript web framework** (Веб-платформа без JavaScript) без изменений и нажмите клавишу ВВОД.

  ![Значения класса GraphHttpClient, которые необходимо ввести в командной строке](../images/graphhttpclient-web-part-create.jpg)

5. Генератор Yeoman создаст веб-часть. Когда шаблон будет сформирован, откройте папку проекта в редакторе кода. В этой статье в инструкциях и на снимках экрана используется Visual Studio Code, но вы можете использовать любой другой редактор.

6. Выполните команду gulp serve и подтвердите, что она правильно выполняется на рабочем месте.

  ```
  gulp serve
  ```

### <a name="add-a-button-and-placeholder-for-results"></a>Добавление кнопки и заполнителя для результатов

Далее вы измените HTML-код и добавите кнопку для получения групп Office 365. В HTML-код также необходимо добавить заполнитель для отображения групп.

1. В редакторе кода откройте файл **/src/webparts/helloGraph/HelloGraphWebPart.ts**.

2. Измените метод **render()** так, чтобы он содержал кнопку и раздел **div**, в котором код будет отображать группы Office 365 после их получения.

  Ваш код должен выглядеть, как указанный ниже TypeScript.

  ```typescript
    public render(): void {
      this.domElement.innerHTML = `
        <div class="${styles.helloGraph}">
        <div class="${styles.container}">
        <div class="ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}">
          <div class="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
            <span class="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
            <p class="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
            <p class="ms-font-l ms-fontColor-white">${escape(this.properties.description)}</p>
            <a href="https://aka.ms/spfx" class="${styles.button}">
              <span class="${styles.label}">Learn more</span>
            </a>
            <p>
            <input id="readGroups" type="button" value="Read Groups"/> 
            </p>
            <div id="spTableContainer" ></div>
          </div>
        </div>
      </div>
    </div>`;
    this.domElement.querySelector('#readGroups').addEventListener('click',() => {this._readGroups();});
    }
  ```

  Вы определите метод **_readGroups()** позже.

3. Определите интерфейс для представления каждой группы Office 365. Добавьте указанный ниже код непосредственно перед классом **HelloGraphWebPart**, но после операций импорта.

  ```typescript
  export interface IOffice365Group {
    // Microsoft Graph has more group properties.
    displayName: string;
    mail: string;
    description: string;
  }
  ```

### <a name="use-the-graphhttpclientget-method-to-retrieve-office-365-groups"></a>Получение групп Office 365 с помощью метода GraphHttpClient.get

Далее вы вызовете метод **GraphHttpClient.get()**, чтобы совершить вызов REST к Microsoft Graph и получить список групп Office 365.

1. Импортируйте класс **GraphHttpClient** и связанные с ним типы, добавив указанный оператор импорта в начале файла **HelloGraphWebPart.ts**.

  ```typescript
  import { GraphHttpClient, HttpClientResponse, IGraphHttpClientOptions } from '@microsoft/sp-http';
  ```

2. Создайте метод **_readGroups()**, добавив указанный ниже код в класс **HelloGraphWebPart**.

  ```typescript
  protected _readGroups(){
      // Query for all groups on the tenant using Microsoft Graph.
      this.context.graphHttpClient.get(`v1.0/groups?$orderby=displayName`, GraphHttpClient.configurations.v1).then((response: HttpClientResponse) => {
        if (response.ok) {
          return response.json();
        } else {
          console.warn(response.statusText);
        }
      }).then((result: any) => {
        // Transfer result values to the group variable
        this._renderTable(result.value);
      });
  }
  ```

  В предыдущем фрагменте кода у свойства контекста имеется экземпляр класса GraphHttpClient. Когда вы вызываете метод **get()**, выполняется вызов REST к Microsoft Graph, который передает указанный URL-адрес. В данном случае используется следующий URL-адрес: **v1.0/groups?orderby=displayName**. В результате создается запрос GET, и Microsoft Graph возвращает все группы Office 365 в клиенте, отсортированные по отображаемому имени.

  Вы можете создать любой запрос GET, использовав этот метод и введя правильные значения URL-адреса. Значения URL-адресов см. в [документации по Microsoft Graph](https://developer.microsoft.com/ru-RU/graph/docs/concepts/overview). Например, для получения групп можно использовать URL-адрес, указанный в [этой статье](https://developer.microsoft.com/ru-RU/graph/docs/api-reference/v1.0/api/group_get). 

  Метод **get()** возвращает объект **HttpClientResponse**, который позволяет определить, успешно ли выполнен вызов. Возвращенный объект JSON находится в объекте **result.value**. Так как вы ожидаете получить несколько групп, вы передаете значение в метод **_renderTable()**, который создает таблицу строк для каждой группы.

3. Создайте метод **_renderTable()** для отображения возвращенных групп в таблице, в которой каждая строка представляет отдельную группу. Добавьте указанный ниже метод в класс **HelloGraphWebPart**.

  ```typescript
  protected _renderTable(items: IOffice365Group[]): void {
    let html: string = '';
    if (items.length<=0){
      html=`<p>There are no groups to list...</p>`;
    }
    else {
      html += `
      <table><tr>
        <th>Display Name</th>
        <th>Mail</th>
        <th>Description</th></tr>`;
      items.forEach((item: IOffice365Group) => {
        html += `
          <tr>
              <td>${item.displayName}</td>
              <td>${item.mail}</td>
              <td>${item.description}</td>
          </tr>`;
      });
      html += `</table>`;
    }
    const tableContainer: Element = this.domElement.querySelector('#spTableContainer');
    tableContainer.innerHTML = html;
    return;
  }
  ```

### <a name="run-the-web-part-to-call-microsoft-graph"></a>Запуск веб-части для вызова Microsoft Graph

Коду необходимо вызвать приложение **GraphHttpClient**, которое выполняется в SharePoint, поэтому вам не удастся запустить его на локальном рабочем месте. Вам придется упаковать и развернуть его в SharePoint.

1. Упакуйте решение с помощью команды gulp.

  ```
  gulp package-solution
  ```

2. Разверните решение в своем клиенте SharePoint, выполнив указанные ниже действия.
  * Перейдите в каталог приложений вашего сайта.
  * Отправьте или перетащите файл **hellograph-webpart.sppkg** в каталог приложений.
  * Если вы доверяете **hellograph-webpart-client-side-solution**, выберите **Сделать это решение доступным для всех сайтов в организации** и нажмите кнопку **Развернуть**.

3. Разместите веб-часть с помощью команды gulp serve.

  ```
  gulp serve --nobrowser
  ```

4. Добавьте веб-часть на веб-страницу или используйте SharePoint Workbench.

  Страница должна выглядеть следующим образом:

  ![Веб-часть GraphHttpClient с кнопкой чтения групп и одной группой в таблице](../images/graphhttpclient-read-groups-display.jpg)

  Если вы нажмете кнопку **Read Groups** (Прочитать группы), отобразится список всех групп Office 365 в вашем клиенте. Если в списке нет ни одной группы, отобразится сообщение, в котором будет указано, что нет ни одной группы. Далее вы создадите группу.

## <a name="create-a-new-office-365-group-using-a-post-call"></a>Создание группы Office 365 с помощью вызова POST

Вы можете совершать вызовы POST к API Microsoft Graph, используя метод **GraphHttpClient.post()**. Вы создадите группу Office 365, используя метод **post()**.


### <a name="add-a-button-and-placeholder-for-results"></a>Добавление кнопки и заполнителя для результатов

Чтобы добавить кнопку для создания группы, изменить HTML-код.

1. В редакторе кода откройте файл **/src/webparts/helloGraph/HelloGraphWebPart.ts**.

2. Измените метод **render()** так, чтобы он содержал кнопку и раздел **div**, который будет сигнализировать об успешности создания группы.

  Ваш код должен выглядеть, как указанный ниже TypeScript.

  ```typescript
    public render(): void {
      this.domElement.innerHTML = `
        <div class="${styles.helloGraph}">
        <div class="${styles.container}">
        <div class="ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}">
          <div class="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
            <span class="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
            <p class="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
            <p class="ms-font-l ms-fontColor-white">${escape(this.properties.description)}</p>
            <a href="https://aka.ms/spfx" class="${styles.button}">
              <span class="${styles.label}">Learn more</span>
            </a>
            <p>
            <input id="readGroups" type="button" value="Read Groups"/> 
            <input id="createGroup" type="button" value="Create New Group"/>                           
            </p>
            <div id="spCreateGroupResults" ></div>
            <div id="spTableContainer" ></div>
          </div>
        </div>
      </div>
    </div>`;
    this.domElement.querySelector('#createGroup').addEventListener('click',() => {this._createGroup();});
    this.domElement.querySelector('#readGroups').addEventListener('click',() => {this._readGroups();});    
    }
  ```

3. Добавьте метод **_createGroup()** для вызова API Microsoft Graph и создания группы.

  ```typescript
    protected _createGroup(){
      // Use Microsoft Graph to create a sample group.
      this.context.graphHttpClient.post(`v1.0/groups`,GraphHttpClient.configurations.v1,{
        body: JSON.stringify({"description": "Self help community for library",
        "displayName": "Library Assist",
        "groupTypes": [
          "Unified"
        ],
        "mailEnabled": true,
        "mailNickname": "library",
        "securityEnabled": false
      })
    }).then((response: HttpClientResponse) => {
      const resultContainer: Element = this.domElement.querySelector('#spCreateGroupResults');
        if (response.ok) {
          resultContainer.innerHTML = `<p>Sample group created</p>`;
        } else {
          resultContainer.innerHTML = `<p>Could not create group see console for details</p>`;        
          console.warn(response.status);
        }
      });
    }
  ```

  Показанный выше код создает простую группу, используя пример кода из статьи [Создание группы](https://developer.microsoft.com/ru-RU/graph/docs/api-reference/v1.0/api/group_post_groups), посвященной Microsoft Graph.

  Метод **post()** совершает вызов REST API POST по URL-адресу **v1.0/groups**. Третий параметр — значение **IGraphHttpClientOptions**, в котором указано тело JSON для описания новой группы. Класс **HttpClientResponse** используется для определения успешности выполнения вызова и для отображения соответствующего результата.

  Вы можете совершить вызов POST из документации по Microsoft Graph, использовав этот шаблон и указав объект JSON в теле.

### <a name="run-the-web-part-to-create-a-new-group"></a>Запуск веб-части для создания группы

1. Упакуйте решение с помощью команды gulp.

  ```
  gulp package-solution
  ```

2. Разверните решение в своем клиенте SharePoint, выполнив указанные ниже действия.
  * Перейдите в каталог приложений вашего сайта.
  * Отправьте или перетащите файл **hellograph-webpart.sppkg** в каталог приложений.
  * Так как ваше решение уже зарегистрировано, система спросит, следует ли его заменить. Нажмите **Заменить**.
  * Когда система спросит, доверяете ли вы решению, выберите **Развернуть**.

3. Разместите веб-часть с помощью команды gulp serve.

  ```
  gulp serve --nobrowser
  ```

4. Добавьте веб-часть на веб-страницу или используйте SharePoint Workbench.

  Страница должна выглядеть следующим образом:

  ![Веб-часть GraphHttpClient с кнопкой создания группы и сообщением о том, что группа успешно создана](../images/graphhttpclient-group-created.jpg)

5. При нажатии кнопки **Create New Group** код создает группу Office 365. 

  > [!NOTE] 
  > При повторной попытке создать ту же группу код возвращает ошибку, так как группа уже существует. Ошибка записывается в консоли, которую можно просмотреть в режиме разработчика в браузере.

## <a name="update-a-group-using-a-patch-call"></a>Изменение группы с помощью вызова PATCH

К данному моменту вы должны были разобраться в шаблоне. Если вам необходимо совершить вызов к REST API Microsoft Graph, используйте для запроса метод **get()** или **post()** с URL-адресом. Последний метод, о котором следует рассказать, — метод **fetch()**. С помощью этого метода вы можете создать запрос PATCH к Microsoft Graph для изменения ресурса.

В коде ниже показано, как вызвать метод **fetch()** для изменения существующей группы.

```typescript
    this.context.graphHttpClient.fetch(`v1.0/groups/2dfead70-21e4-4f30-bb2b-94b1bbdefdfa`,GraphHttpClient.configurations.v1,{
      method: "PATCH",
      body: JSON.stringify(
        {
          "description": "This is the new description",
          "displayName": "testtest"
        })
  }).then((response: HttpClientResponse) => {
    const resultContainer: Element = this.domElement.querySelector('#spUpdateGroupResults');
      if (response.ok) {
        resultContainer.innerHTML = `<p>Group updated</p>`;
      } else {
        resultContainer.innerHTML = `<p>Could not update group see console for details</p>`;        
        console.warn(response.status);
      }
    });
```

Идентификатор группы указан в URL-адресе. Получите идентификатор, выполнив сначала вызов GET. Параметр **method** имеет значение **PATCH**. В теле указано, свойства какой группы необходимо изменить.

## <a name="see-also"></a>См. также

- [Обзор класса GraphHttpClient](overview-graphhttpclient.md)
