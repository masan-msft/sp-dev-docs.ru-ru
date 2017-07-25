<span data-ttu-id="26884-p130">**Утечки из неограниченных классов**: еще одна проблема с селекторами потомков. Обратите внимание, что в приведенном выше примере стили высоты и ширины из неограниченного класса myButton применяются ко всем кнопкам. Это означает, что изменение этого стиля может случайно сделать неработоспособным код HTML, в котором используется разметка с ограниченной областью действия. Допустим, по какой-то причине на уровне приложения мы меняем высоту в классе myButton на 0 пикселей. В результате во всех сторонних веб-частях, использующих класс myButton, будет задана высота в 0 пикселей, что отрицательно скажется на пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="26884-p130">**Leakage from unscoped classes** - There is another problem with descendant selectors. Note in the above example, the height and the width styles from the unscoped myButton class are applied to all the buttons. This implies that a change in that style could inadvertently break html using scoped markup. Say for example, for some reason at the app level we decide to make height 0px on the myButton class. That will result in all 3rd party web parts using the myButton class to have a height of 0 i.e. a serious regression in the user experience.</span></span>

```HTML
  <html>
  <head>
  <title>CSS specifity test</title>
  <style>
  .myButton {
      background-color: brown;
      color:brown;
      height:20px;
      width:40px;
  }
  </style>
  <style>
  .scope2 .myButton {
      background-color: green;
      color:green;
  }
  </style>
  <style>
  .scope3 .myButton {
      background-color: yellow;
      color:yellow;
  }
  </style>
  <style>
  .scope1 .myButton {
      background-color: red;
      color:red;
  }
  </style>
</head>
<body>
  <div>
    <span>These tests demonstrate descendant selectors, nesting and load order problems.</span>

    <div>
      <br/>
      <span>This test depicts that a descendant selector with the same specificity do not allow nesting.
      All buttons below do not take the innermost scope i.e. they should be different colors, but they are red.
      Further, if you change the ordering of the style tags, the colors will change. i.e. the UI is load order dependant.</span> 
      <div class='scope1'>
        <button class='myButton'</button>
        <div class='scope2'>
          <button class='myButton'></button>
          <div class='scope3'>
            <button class='myButton'></button>
          </div>
        </div>
      </div>
    </div>
  </div>
</body>
</html>
```

**Утечки из неограниченных классов**: еще одна проблема с селекторами потомков. Обратите внимание, что в приведенном выше примере стили высоты и ширины из неограниченного класса myButton применяются ко всем кнопкам. Это означает, что изменение этого стиля может случайно сделать неработоспособным код HTML, в котором используется разметка с ограниченной областью действия. Допустим, по какой-то причине на уровне приложения мы меняем высоту в классе myButton на 0 пикселей. В результате во всех сторонних веб-частях, использующих класс myButton, будет задана высота в 0 пикселей, что отрицательно скажется на пользовательском интерфейсе.

## <a name="updating-an-existing-project"></a><span data-ttu-id="26884-232">Обновление существующего проекта</span><span class="sxs-lookup"><span data-stu-id="26884-232">Updating an existing project</span></span>

<span data-ttu-id="26884-233">В файле `package.json` проекта обновите зависимость `@microsoft/sp-build-web` до версии 1.0.1 или выше, удалите каталог `node_modules` проекта и выполните команду `npm install`.</span><span class="sxs-lookup"><span data-stu-id="26884-233">In your project's `package.json`, update the `@microsoft/sp-build-web` dependency to at least version 1.0.1, delete your project's `node_modules` directory, and run `npm install`.</span></span>

