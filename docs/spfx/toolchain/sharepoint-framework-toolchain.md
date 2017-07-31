<span data-ttu-id="063e4-p121">Обычно, когда проект веб-части готов к отгрузке или развертыванию на рабочем сервере, используется целевой режим SHIP. Для других сценариев, например проверки и отладки, используется целевой режим BUILD. Целевой режим SHIP также гарантирует, что выполнена сборка минифицированной версии пакета веб-части.</span><span class="sxs-lookup"><span data-stu-id="063e4-p121">Usually, when your web part project is ready to ship or deploy in a production server, you will target SHIP. For other scenarios like testing and debugging you would target BUILD. The SHIP target also ensures that the minified version of the web part bundle is built.</span></span>

Обычно, когда проект веб-части готов к отгрузке или развертыванию на рабочем сервере, используется целевой режим SHIP. Для других сценариев, например проверки и отладки, используется целевой режим BUILD. Целевой режим SHIP также гарантирует, что выполнена сборка минифицированной версии пакета веб-части. 

<span data-ttu-id="063e4-219">Чтобы использовать режим SHIP, добавьте к имени задачи `--ship`:</span><span class="sxs-lookup"><span data-stu-id="063e4-219">To target SHIP mode, you append the task with `--ship`:</span></span>

```
gulp --ship
```

<span data-ttu-id="063e4-220">В режиме DEBUG задачи сборки копируют все ресурсы веб-части, в том числе пакет веб-части, в папку `dist`.</span><span class="sxs-lookup"><span data-stu-id="063e4-220">In DEBUG mode, the build tasks copy all of the web part assets, including the web part bundle, into the `dist` folder.</span></span>

<span data-ttu-id="063e4-221">В режиме SHIP задачи сборки копируют все ресурсы веб-части, в том числе пакет веб-части, в папку `temp\deploy`.</span><span class="sxs-lookup"><span data-stu-id="063e4-221">In SHIP mode, the build tasks copy all of the web part assets, including the web part bundle, into the `temp\deploy` folder.</span></span>
