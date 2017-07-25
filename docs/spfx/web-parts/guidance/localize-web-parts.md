<span data-ttu-id="0cf55-p145">При загрузке веб-части на странице SharePoint Framework автоматически загрузит файл ресурсов для соответствующего языкового стандарта, используя информацию с сайта контекста. Если соответствующий файл ресурсов не будет найден, SharePoint Framework загрузит файл, указанный в свойстве **defaultPath**. Отдельные файлы ресурсов позволяют SharePoint Framework загружать на странице только данные для языкового стандарта, используемого на сайте.</span><span class="sxs-lookup"><span data-stu-id="0cf55-p145">When loading the web part on the page, the SharePoint Framework will automatically load the resource file for the corresponding locale by using the information from the context site. If no matching resource file is found, the SharePoint Framework will load the file specified in the **defaultPath** property. By keeping the resource files separate, the SharePoint Framework minimizes the amount of data loaded on the page to the locale that matches the one used in the site.</span></span>

```json
{
  "id": "edbc4e31-6085-4ffa-85f4-eeffcb0ea2d4",
  "alias": "GreetingWebPart",
  "componentType": "WebPart",
  "version": "0.0.1",
  "manifestVersion": 2,
  // ...
  "loaderConfig": {
    "entryModuleId": "greeting.bundle",
    "internalModuleBaseUrls": [
      "https://cdn.contoso.com/"
    ],
    "scriptResources": {
      "greeting.bundle": {
        "type": "internal",
        "path": "greeting.bundle_734e78a24ec5779bbc7a5a10603d4904.js"
      },
      "greetingStrings": {
        "defaultPath": "react-localization-greetingstrings_en-us_60a6b3dba7cc244bcc28781a2e292f85.js",
        "type": "localized",
        "paths": {
          "en-US": "react-localization-greetingstrings_en-us_60a6b3dba7cc244bcc28781a2e292f85.js",
          "nl-NL": "react-localization-greetingstrings_nl-nl_ecae5f3385f9e9bef23817b91d1a0bf1.js",
          "qps-ploc": "react-localization-greetingstrings_qps-ploc_dc97c611a9edc88818c84871f3749afb.js"
        }
      },
      // ...
    }
  }
}
```

При загрузке веб-части на странице SharePoint Framework автоматически загрузит файл ресурсов для соответствующего языкового стандарта, используя информацию с сайта контекста. Если соответствующий файл ресурсов не будет найден, SharePoint Framework загрузит файл, указанный в свойстве **defaultPath**. Отдельные файлы ресурсов позволяют SharePoint Framework загружать на странице только данные для языкового стандарта, используемого на сайте.