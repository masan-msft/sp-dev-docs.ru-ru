<span data-ttu-id="36845-p131">Универсальная ненастроенная версия веб-части добавится к конфигурациям для определенных сценариев. Таким образом, если для потребностей пользователя нет соответствующей конфигурации, он может выбрать универсальную версию и настроить ее по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="36845-p131">The generic unconfigured version of the web part is added beside the configurations that target specific scenarios. This way, if there is no specific configuration addressing users' needs, they can always use the generic version and configure it according to their requirements.</span></span>

```json
{
  // ...
  "preconfiguredEntries": [{
    "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
    "group": { "default": "Content" },
    "title": { "default": "Recent images" },
    "description": { "default": "Shows 5 most recent images" },
    "officeFabricIconFontName": "Picture",
    "properties": {
      "listName": "Images",
      "order": "reversed",
      "numberOfItems": 5,
      "style": "thumbnails"
    }
  },
  {
    "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
    "group": { "default": "Content" },
    "title": { "default": "Recent documents" },
    "description": { "default": "Shows 10 most recent documents" },
    "officeFabricIconFontName": "Documentation",
    "properties": {
      "listName": "Documents",
      "order": "reversed",
      "numberOfItems": 10,
      "style": "list"
    }
  },
  {
    "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
    "group": { "default": "Content" },
    "title": { "default": "Gallery" },
    "description": { "default": "Shows items from the selected list" },
    "officeFabricIconFontName": "CustomList",
    "properties": {
      "listName": "",
      "order": "",
      "numberOfItems": 5,
      "style": ""
    }
  }]
}
```

Универсальная ненастроенная версия веб-части добавится к конфигурациям для определенных сценариев. Таким образом, если для потребностей пользователя нет соответствующей конфигурации, он может выбрать универсальную версию и настроить ее по своему усмотрению.

<span data-ttu-id="36845-255">Чтобы увидеть результат, запустите отладку проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="36845-255">To see the result start debugging the project by running the following command:</span></span>

```sh
gulp serve
```

<span data-ttu-id="36845-256">Открыв панель элементов веб-частей для добавления веб-части на холст, вы увидите, что теперь пользователь может выбрать одну из трех веб-частей.</span><span class="sxs-lookup"><span data-stu-id="36845-256">When you open the web part toolbox to add the web part to the canvas, you will see that there are now three web parts that users can choose from.</span></span>

![Панель элементов веб-частей с предварительно настроенной версией веб-части](../../../../images/preconfiguredentries-three-configurations-toolbox.png)