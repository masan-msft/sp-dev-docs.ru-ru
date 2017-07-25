<span data-ttu-id="9819f-p113">Наконец, введите в консоли команду gulp serve, чтобы открыть локальное рабочее место, которое теперь будет работать с фиктивными данными. (Если у вас уже запущен сервер, остановите его с помощью клавиш CTRL+C, а затем снова запустите.)</span><span class="sxs-lookup"><span data-stu-id="9819f-p113">Finally type gulp serve in the console to bring up the local workbench, which now will work with the mock data. (If you already have the server running stop it using Ctrl+C and then restart it)</span></span>

```TypeScript
private _registerComponent(tagName: string): void {

  if (Environment.type === EnvironmentType.Local) {
    console.log("here I am.")
    ko.components.register(
      tagName,
      {
        viewModel: MockSpPnPjsExampleViewModel,
        template: require('./SpPnPjsExample.template.html'),
        synchronous: false
      }
    );
  } else {
    ko.components.register(
      tagName,
      {
        viewModel: SpPnPjsExampleViewModel,
        template: require('./SpPnPjsExample.template.html'),
        synchronous: false
      }
    );
  }
}
```
Наконец, введите в консоли команду gulp serve, чтобы открыть локальное рабочее место, которое теперь будет работать с фиктивными данными. (Если у вас уже запущен сервер, остановите его с помощью клавиш CTRL+C, а затем снова запустите.)

```sh
gulp serve
```

![Проект, запущенный на локальном рабочем месте с фиктивными данными](../../../../images/sp-pnp-js-guide-with-mock-data.png)


## <a name="download-full-example-code"></a><span data-ttu-id="9819f-169">Полный пример кода</span><span class="sxs-lookup"><span data-stu-id="9819f-169">Download Full Example Code</span></span>

<span data-ttu-id="9819f-170">Помните, что вы можете скачать полный пример кода [здесь](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/knockout-sp-pnp-js).</span><span class="sxs-lookup"><span data-stu-id="9819f-170">Remember you can find the full sample [here](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/knockout-sp-pnp-js).</span></span>

## <a name="provide-feedback--report-issues"></a><span data-ttu-id="9819f-171">Отзывы и отчеты о неполадках</span><span class="sxs-lookup"><span data-stu-id="9819f-171">Provide Feedback / Report Issues</span></span>

<span data-ttu-id="9819f-172">Если у вас есть отзывы или вы хотите сообщить о проблеме с библиотекой sp-pnp-js, используйте [список проблем](https://github.com/SharePoint/PnP-JS-Core/issues) в этом репозитории.</span><span class="sxs-lookup"><span data-stu-id="9819f-172">If you have any feedback or need to report as issue with sp-pnp-js please use the [issues list](https://github.com/SharePoint/PnP-JS-Core/issues) in that repo.</span></span>
