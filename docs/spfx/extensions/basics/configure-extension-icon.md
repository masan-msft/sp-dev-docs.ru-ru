---
title: "Настройка значков в расширениях SharePoint Framework (SPFx)"
description: "Способы настройки значков для команд в расширениях SharePoint (SPFx)."
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: 1dcbef078f8985de00614f8ebfbf3dd1030439d6
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2018
---
# <a name="configure-extension-icon"></a>Настройка значка расширения

Значок, иллюстрирующий назначение вашей пользовательской команды в SharePoint Framework, поможет пользователям найти ее среди других элементов на панели инструментов или в контекстном меню. Указывать значок для команды необязательно. Если значок не задан, на панели команд отображается только название команды.

SharePoint Framework поддерживает создание расширений следующих типов:

- настройщик заполнителей;
- настройщик полей;
- набор команд.

Набор команд — единственный тип расширения SharePoint Framework, для которого можно настраивать значки.

При развертывании наборов команд можно выбрать, где должны отображаться соответствующие команды:

- на панели команд (`location: ClientSideExtension.ListViewCommandSet.CommandBar`);

- в контекстном меню (`location: ClientSideExtension.ListViewCommandSet.ContextMenu`);

- в обоих местах (`location: ClientSideExtension.ListViewCommandSet`).

Значки, определенные для разных команд, отображаются только на панели команд.

В SharePoint Framework доступно два способа определения значков для расширений:

- Использование внешнего изображения
- Использование изображения в кодировке base64

## <a name="use-an-external-icon-image"></a>Использование внешнего изображения

При создании наборов команд SharePoint Framework вы можете задать значок для каждой команды, указав абсолютный URL-адрес, указывающий на изображение в манифесте расширения, с помощью свойства **iconImageUrl**.

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx/command-set-extension-manifest.schema.json",

  "id": "6cdfbff6-714f-4c26-a60c-0b18afe60837",
  "alias": "WeatherCommandSet",
  "componentType": "Extension",
  "extensionType": "ListViewCommandSet",

  // The "*" signifies that the version should be taken from the package.json
  "version": "*",
  "manifestVersion": 2,

  // If true, the component can only be installed on sites where Custom Script is allowed.
  // Components that allow authors to embed arbitrary script code should set this to true.
  // https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f
  "requiresCustomScript": false,

  "items": {
    "WEATHER": {
      "title": { "default": "Weather" },
      "iconImageUrl": "https://localhost:4321/temp/sun.png",
      "type": "command"
    }
  }
}
```

<br/>

Размер значка команды, отображаемого на панели команд, составляет 16x16 пикселей. Если указано изображение большего размера, оно будет уменьшено с сохранением пропорций.

![Пользовательское изображение, используемое в качестве значка команды на панели команд](../../../images/extensionicon_commandbar_imagepng.png)

<br/>

Использование пользовательских изображений обеспечивает широкие возможности выбора значка для команды, но при этом их требуется развертывать вместе с другими ресурсами расширения. Кроме того, качество изображения может снизиться при использовании высокого разрешения или некоторых специальных возможностей. Во избежание снижения качества можно использовать векторные изображения в формате SVG, которые также поддерживаются на платформе SharePoint Framework.

## <a name="use-a-base64-encoded-image"></a>Использование изображения в кодировке base64

При использовании пользовательского изображения можно не указывать абсолютный URL-адрес файла изображения, размещенного вместе с другими ресурсами расширения, а закодировать изображение в формате base64 и использовать строку base64 вместо URL-адреса.

В Интернете есть ряд служб, позволяющих закодировать изображение в формате base64, например [эта](https://www.base64-image.de).

После кодирования изображения скопируйте строку base64 и используйте ее в качестве значения свойства **iconImageUrl** в манифесте веб-части.

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx/command-set-extension-manifest.schema.json",

  "id": "6cdfbff6-714f-4c26-a60c-0b18afe60837",
  "alias": "WeatherCommandSet",
  "componentType": "Extension",
  "extensionType": "ListViewCommandSet",

  // The "*" signifies that the version should be taken from the package.json
  "version": "*",
  "manifestVersion": 2,

  // If true, the component can only be installed on sites where Custom Script is allowed.
  // Components that allow authors to embed arbitrary script code should set this to true.
  // https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f
  "requiresCustomScript": false,

  "items": {
    "WEATHER": {
      "title": { "default": "Weather" },
      "iconImageUrl": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAQAAAAEACAYAAABccqhmAAAAAXNSR0IB2cksfwAAACBjSFJNAAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAB/hUlEQVR42u29ebwkWVUn/j03Ipe31PZqr+ruqu7q6pXuZlcRRgUVBRnUn0rpMAJuTDeLog4u48bMiDoMtCA0MjAwOqil4oI6qCO2oIiDTQ...",
      "type": "command"
    }
  }
}
```

<br/>

Кодировка base64 подходит как для растровых изображений (например, PNG-файлов), так и для векторных изображений в формате SVG. Главное преимущество использования изображений в кодировке base64 заключается в том, что значок веб-части не нужно развертывать отдельно.

![Изображение в кодировке base64, отображаемое в качестве значка веб-части на панели элементов](../../../images/extensionicon_commandbar_base64.png)

## <a name="see-also"></a>См. также

- [Обзор расширений SharePoint Framework](../overview-extensions.md)