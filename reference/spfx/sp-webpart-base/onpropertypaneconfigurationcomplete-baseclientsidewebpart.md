# <a name="onpropertypaneconfigurationcomplete"></a>onPropertyPaneConfigurationComplete()




Этот API вызывается после завершения настройки PropertyPane. Он вызывается в следующих случаях: – Когда истекает время CONFIGURATION_COMPLETE_TIMEOUT((текущее значение — 5 секунд) после последнего изменения. – Когда пользователь нажимает кнопку "x" (закрыть) до истечения времени CONFIGURATION_COMPLETE_TIMEOUT. – Когда пользователь нажимает кнопку "Применить" до истечения времени CONFIGURATION_COMPLETE_TIMEOUT. – Когда пользователь открывает другую веб-часть, тогда текущая веб-часть получает это событие.

**Подпись:** _@virtual protected onPropertyPaneConfigurationComplete(): void;_

**Возвращаемое значение**: `void`





#### <a name="parameters"></a>Параметры
Нет


