<span data-ttu-id="1c5f2-p113">Добавьте к URL-адресу приведенные ниже параметры строки запроса. Обратите внимание, что вам потребуется обновить параметр **id** в соответствии с идентификатором расширения, указанным в файле **DialogDemoCommandSet.manifest.json**:</span><span class="sxs-lookup"><span data-stu-id="1c5f2-p113">Append the following query string parameters to the URL. Notice that you will need to update the **id** to match your own extension identifier available from the **DialogDemoCommandSet.manifest.json** file:</span></span> 

Добавьте к URL-адресу приведенные ниже параметры строки запроса. Обратите внимание, что вам потребуется обновить параметр **id** в соответствии с идентификатором расширения, указанным в файле **DialogDemoCommandSet.manifest.json**:

```
?loadSpfx=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"8701f44c-8c81-4e54-999d-62763e8f34d2":{"location":"ClientSideExtension.ListViewCommandSet.CommandBar"}}
```

<span data-ttu-id="1c5f2-176">Согласитесь на загрузку манифестов отладки, нажав кнопку **Загрузить скрипты отладки** при появлении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="1c5f2-176">Accept the loading of Debug Manifests by clicking **Load debug scripts** when prompted:</span></span>

![Предупреждение о разрешении скриптов отладки](../../../../images/ext-com-dialog-debug-scripts.png)

<span data-ttu-id="1c5f2-178">Обратите внимание на новую кнопку *Open Custom Dialog* (Открыть настраиваемое диалоговое окно) на панели инструментов списка.</span><span class="sxs-lookup"><span data-stu-id="1c5f2-178">Notice new button being visible in the toolbar of the list with test *Open Custom Dialog*.</span></span>

![Предупреждение о разрешении скриптов отладки](../../../../images/ext-com-dialog-button-in-toolbar.png)

<span data-ttu-id="1c5f2-180">Нажмите кнопку *Open Custom Dialog*, чтобы в представлении списка открылось настраиваемое диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="1c5f2-180">Click *Open Custom Dialog* button to see custom dialog rendered in the list view.</span></span> 

![Предупреждение о разрешении скриптов отладки](../../../../images/ext-com-dialog-visible-dialog.png)

<span data-ttu-id="1c5f2-182">Выберите цвет в *палитре* и нажмите кнопку **ОК**, чтобы проверить, как код возвращает вызывающей стороне выбранное значение, которое затем отображается с помощью встроенного диалогового окна предупреждения.</span><span class="sxs-lookup"><span data-stu-id="1c5f2-182">Choose a color in the *Color Picker* and click **OK** to test how the code is returning selected value back to caller, which is then shown using out-of-the-box alert dialog.</span></span>

![Встроенное диалоговое окно предупреждения](../../../../images/ext-com-dialog-oob-alert-dialog.png)
