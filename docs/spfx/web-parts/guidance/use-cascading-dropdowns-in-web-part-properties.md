<span data-ttu-id="9943c-p124">**Примечание.** В выпуске 6 SharePoint Framework допущена ошибка в компоненте Office UI Fabric React Dropdown, из-за которой раскрывающееся меню работает неправильно. Чтобы временно решить эту проблему, измените строку **12027** в файле **node_modules/@microsoft/office-ui-fabric-react-bundle/dist/office-ui-fabric-react.bundle.js**. Исходный вариант:</span><span class="sxs-lookup"><span data-stu-id="9943c-p124">**Note:** In drop 6 of the SharePoint Framework there is a bug in the Office UI Fabric React Dropdown component that causes the dropdown control to work incorrectly. A temporary workaround is to edit the **node_modules/@microsoft/office-ui-fabric-react-bundle/dist/office-ui-fabric-react.bundle.js** file and change line **12027** from:</span></span>

> **Примечание.** В выпуске 6 SharePoint Framework допущена ошибка в компоненте Office UI Fabric React Dropdown, из-за которой раскрывающееся меню работает неправильно. Чтобы временно решить эту проблему, измените строку **12027** в файле **node_modules/@microsoft/office-ui-fabric-react-bundle/dist/office-ui-fabric-react.bundle.js**. Исходный вариант:
> 
> ```js
> isDisabled: this.props.isDisabled !== undefined ? this.props.isDisabled : this.props.disabled
> ```
>
> <span data-ttu-id="9943c-235">на значение:</span><span class="sxs-lookup"><span data-stu-id="9943c-235">to:</span></span>
> 
> ```js
> isDisabled: newProps.isDisabled !== undefined ? newProps.isDisabled : newProps.disabled
> ```

![Раскрывающееся меню на панели свойств веб-части, показывающее доступные элементы выбранного списка](../../../../images/react-cascading-dropdowns-item-dropdown-list-items.png)
